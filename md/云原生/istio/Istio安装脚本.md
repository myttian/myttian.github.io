# Istio

[Istio 下载](https://istio.io/latest/zh/docs/setup/getting-started/#download)    [ Poe翻译](https://poe.com/chat/3f0ge98si41ettazaj9)

这个脚本是用来下载和安装 Istio 服务网格的最新版本。以下是对脚本各部分的解释:

1. set -e: 如果任何命令返回非零退出状态,整个脚本将会退出。
2. 确定操作系统类型(OS)和相应的扩展名(OSEXT)。
3. 如果没有设置 ISTIO_VERSION 环境变量,则自动获取最新版本号。
4. 根据操作系统架构设置 ISTIO_ARCH 变量。支持 amd64、arm64 和 armv7。
5. 如果没有设置 ISTIO_VERSION，则退出并提示用户设置此变量。
6. 构建下载 URL。有两种情况:
   1. 如果架构支持,使用带有架构信息的 URL。
   2. 如果架构不支持,使用不带架构信息的 URL。
7. 根据操作系统和 Istio 版本,决定使用哪种下载方式:
   1. 对于 Linux,如果 Istio 版本小于 1.6,使用不带架构的下载方式,否则使用带架构的下载方式。
   2. 对于 macOS,如果 Istio 版本小于 1.10 或者架构不是 arm64,使用不带架构的下载方式,否则使用带架构的下载方式。
   3. 对于其他操作系统,退出并提示用户。
8. 下载并解压缩 Istio 压缩包,删除压缩包文件。

总之,这个脚本旨在自动下载并安装适合当前操作系统和架构的 Istio 最新版本,提高了安装 Istio 的便利性。

```sh
curl -L https://istio.io/downloadIstio | sh -
# 获得版本号：  releases/1.22.2/ 
ISTIO_VERSION="$(curl -sL https://github.com/istio/istio/releases |  grep -o 'releases/[0-9]*.[0-9]*.[0-9]*/' | sort -V |  tail -1 | awk -F'/' '{ print $2}')"

使用 curl 命令从 GitHub 上获取 Istio 发布页面的内容。
使用 grep 命令从页面内容中找到所有版本号格式为 releases/X.Y.Z/ 的字符串。
使用 sort -V 命令对版本号进行升序排序,这样最新的版本号会排在最后。
使用 tail -1 命令获取排序后的最后一个版本号,也就是最新版本号。
使用 awk 命令从完整的版本号路径中提取出纯粹的版本号,例如 "1.22.2"。
最后将获取到的最新版本号输出到终端。

# 从 ISTIO_VERSION 变量中提取出纯粹的版本号,去掉了前面的 "releases/" 部分
ISTIO_VERSION="${ISTIO_VERSION##*/}"	

${ISTIO_VERSION##*/} 是一种 Bash 中的字符串操作语法,称为"最长模式删除"。
##*/ 表示从变量值的右侧开始删除,删除到最后一个 "/" 字符及其左侧的所有内容。		#  releases/1.22.2/ 
这样就可以从类似 "releases/1.22.2/" 这样的字符串中提取出纯粹的版本号 "1.22.2"。

```



```shell
#!/bin/sh

# Copyright Istio Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

#
# This file will be fetched as: curl -L https://git.io/getLatestIstio | sh -
# so it should be pure bourne shell, not bash (and not reference other scripts)
#
# The script fetches the latest Istio release candidate and untars it.
# You can pass variables on the command line to download a specific version
# or to override the processor architecture. For example, to download
# Istio 1.6.8 for the x86_64 architecture and linux OS,
# run curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.6.8 TARGET_ARCH=x86_64 TARGET_OS=Linux sh -.

set -e

# Determines the operating system.
OS="${TARGET_OS:-$(uname)}"
if [ "${OS}" = "Darwin" ] ; then
  OSEXT="osx"
else
  OSEXT="linux"
fi

# Determine the latest Istio version by version number ignoring alpha, beta, and rc versions.
if [ "${ISTIO_VERSION}" = "" ] ; then
  ISTIO_VERSION="$(curl -sL https://github.com/istio/istio/releases | \
                  grep -o 'releases/[0-9]*.[0-9]*.[0-9]*/' | sort -V | \
                  tail -1 | awk -F'/' '{ print $2}')"
  ISTIO_VERSION="${ISTIO_VERSION##*/}"
fi

LOCAL_ARCH=$(uname -m)
if [ "${TARGET_ARCH}" ]; then
    LOCAL_ARCH=${TARGET_ARCH}
fi

case "${LOCAL_ARCH}" in
  x86_64|amd64)
    ISTIO_ARCH=amd64
    ;;
  armv8*|aarch64*|arm64)
    ISTIO_ARCH=arm64
    ;;
  armv*)
    ISTIO_ARCH=armv7
    ;;
  *)
    echo "This system's architecture, ${LOCAL_ARCH}, isn't supported"
    exit 1
    ;;
esac

if [ "${ISTIO_VERSION}" = "" ] ; then
  printf "Unable to get latest Istio version. Set ISTIO_VERSION env var and re-run. For example: export ISTIO_VERSION=1.0.4"
  exit 1;
fi

NAME="istio-$ISTIO_VERSION"
URL="https://github.com/istio/istio/releases/download/${ISTIO_VERSION}/istio-${ISTIO_VERSION}-${OSEXT}.tar.gz"
ARCH_URL="https://github.com/istio/istio/releases/download/${ISTIO_VERSION}/istio-${ISTIO_VERSION}-${OSEXT}-${ISTIO_ARCH}.tar.gz"

with_arch() {
  printf "\nDownloading %s from %s ...\n" "$NAME" "$ARCH_URL"
  if ! curl -o /dev/null -sIf "$ARCH_URL"; then
    printf "\n%s is not found, please specify a valid ISTIO_VERSION and TARGET_ARCH\n" "$ARCH_URL"
    exit 1
  fi
  curl -fsLO "$ARCH_URL"
  filename="istio-${ISTIO_VERSION}-${OSEXT}-${ISTIO_ARCH}.tar.gz"
  tar -xzf "${filename}"
  rm "${filename}"
}

without_arch() {
  printf "\nDownloading %s from %s ..." "$NAME" "$URL"
  if ! curl -o /dev/null -sIf "$URL"; then
    printf "\n%s is not found, please specify a valid ISTIO_VERSION\n" "$URL"
    exit 1
  fi
  curl -fsLO "$URL"
  filename="istio-${ISTIO_VERSION}-${OSEXT}.tar.gz"
  tar -xzf "${filename}"
  rm "${filename}"
}

# Istio 1.6 and above support arch
# Istio 1.5 and below do not have arch support
ARCH_SUPPORTED="1.6"
# Istio 1.10 and above support arch for osx arm64
ARCH_SUPPORTED_OSX="1.10"

if [ "${OS}" = "Linux" ] ; then
  # This checks if ISTIO_VERSION is less than ARCH_SUPPORTED (version-sort's before it)
  if [ "$(printf '%s\n%s' "${ARCH_SUPPORTED}" "${ISTIO_VERSION}" | sort -V | head -n 1)" = "${ISTIO_VERSION}" ]; then
    without_arch
  else
    with_arch
  fi
elif [ "${OS}" = "Darwin" ] ; then
  # This checks if ISTIO_VERSION is less than ARCH_SUPPORTED_OSX (version-sort's before it) or ISTIO_ARCH not equal to arm64
  if [ "$(printf '%s\n%s' "${ARCH_SUPPORTED_OSX}" "${ISTIO_VERSION}" | sort -V | head -n 1)" = "${ISTIO_VERSION}" ] || [ "${ISTIO_ARCH}" != "arm64" ]; then
    without_arch
  else
    with_arch
  fi
else
  printf "\n\n"
  printf "Unable to download Istio %s at this moment!\n" "$ISTIO_VERSION"
  printf "Please verify the version you are trying to download.\n\n"
  exit 1
fi

printf ""
printf "\nIstio %s Download Complete!\n" "$ISTIO_VERSION"
printf "\n"
printf "Istio has been successfully downloaded into the %s folder on your system.\n" "$NAME"
printf "\n"
BINDIR="$(cd "$NAME/bin" && pwd)"
printf "Next Steps:\n"
printf "See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.\n"
printf "\n"
printf "To configure the istioctl client tool for your workstation,\n"
printf "add the %s directory to your environment path variable with:\n" "$BINDIR"
printf "\t export PATH=\"\$PATH:%s\"\n" "$BINDIR"
printf "\n"
printf "Begin the Istio pre-installation check by running:\n"
printf "\t istioctl x precheck \n"
printf "\n"
printf "Need more information? Visit https://istio.io/latest/docs/setup/install/ \n"
```

