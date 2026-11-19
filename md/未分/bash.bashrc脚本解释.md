

# /etc/bash.bashrc脚本

这段脚本通常出现在Bash shell的初始化文件中，用于设置用户环境和提示符。以下是逐行解释：

1. `[ -z "$PS1" ] && return`: 检查`PS1`（Bash命令提示符）是否为空。如果为空，脚本直接返回，不做进一步处理。

2. `shopt -s checkwinsize`: 启用`checkwinsize`选项，使Bash在会话期间自动调整终端窗口大小。

3. 以下代码块：

   ```bash
   if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
       debian_chroot=$(cat /etc/debian_chroot)
   fi
   
   # 检查`debian_chroot`变量是否未设置，且`/etc/debian_chroot`文件是否可读。如果两者都满足，读取`/etc/debian_chroot`文件的内容并赋值给`debian_chroot`变量。 
   ```

4. 接下来的代码块设置`PS1`提示符：

   ```bash
   if ! [ -n "${SUDO_USER}" -a -n "${SUDO_PS1}" ]; then
       PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
   fi
   
   # 如果SUDO_USER和SUDO_PS1都未设置（意味着用户不是通过sudo运行的shell），它将提示符设置为显示用户、主机名、当前工作目录和美元符号（$）。如果debian_chroot已设置，它会在用户前括号内显示。
   ```

5. 最后这段代码块会在用户具有`admin`或`sudo`组权限时给出使用`sudo`的提示：

   ```sh
   if [ ! -e "$HOME/.sudo_as_admin_successful" ] && [ ! -e "$HOME/.hushlogin" ] ; then
       case " $(groups) " in *\ admin\ *|*\ sudo\ *)
           if [ -x /usr/bin/sudo ]; then
               cat <<-EOF
               要以管理员（用户"root"）身份运行命令，请使用"sudo <命令>"。
               详情见"man sudo_root"。
               
               EOF
           fi
       esac
   fi
   ```

   如果用户之前没有使用过sudo（`通过检查$HOME/.sudo_as_admin_successful文件是否存在`），并且没有禁用登录消息（$HOME/.hushlogin），脚本会检查用户是否属于admin或sudo组。如果用户是，且sudo可执行，脚本将打印一条消息，提示用户使用sudo来以root权限运行命令。

总之，这个脚本设置Bash命令提示符，调整终端窗口大小，并为使用sudo执行管理员任务提供提示信息。



这段脚本主要用于处理命令找不到（command not found）的情况。它检查系统中是否存在用于处理这种错误的程序，然后定义一个名为command_not_found_handle的函数来调用这些程序。以下是逐行解释：

1. if [ -x /usr/lib/command-not-found -o -x /usr/share/command-not-found/command-not-found ]; then: 检查两个路径（/usr/lib/command-not-found 和 /usr/share/command-not-found/command-not-found）中是否存在可执行文件。-x 检查文件是否可执行，-o 表示逻辑或（or）。
2. function command_not_found_handle {: 定义一个名为 command_not_found_handle 的函数。
3. if [ -x /usr/lib/command-not-found ]; then: 检查 /usr/lib/command-not-found 是否可执行。
4. /usr/lib/command-not-found -- "$1": 如果可执行，调用该程序并传入找不到的命令作为参数（$1 代表函数接收到的第一个参数）。
5. return $?: 传回命令执行的退出状态。$? 是上一个命令的退出状态码。
6. elif [ -x /usr/share/command-not-found/command-not-found ]; then: 如果上一个条件不满足，检查 /usr/share/command-not-found/command-not-found 是否可执行。
7. /usr/share/command-not-found/command-not-found -- "$1": 如果可执行，调用该程序并传入找不到的命令。
8. `return $?: `与之前相同，返回退出状态码。
9. else: 如果两个路径中都没有找到可执行文件。
10. printf "%s: command not found\n" "$1" >&2: 使用 printf 打印一条错误消息，表示命令未找到，将消息定向到标准错误输出（>&2）。
11. return 127: 退出状态码 127 通常用于表示命令未找到。
12. fi: 关闭 command_not_found_handle 函数的定义。
13. fi: 结束外层的 if 语句。

当用户尝试运行系统中不存在的命令时，这个函数会被自动调用，提供额外的信息或帮助，而不是简单地输出错误消息。

```sh
[ -z "$PS1" ] && return
shopt -s checkwinsize
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi
if ! [ -n "${SUDO_USER}" -a -n "${SUDO_PS1}" ]; then
  PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi

# 用户具有`admin`或`sudo`组权限时给出使用`sudo`的提示
if [ ! -e "$HOME/.sudo_as_admin_successful" ] && [ ! -e "$HOME/.hushlogin" ] ; then
    case " $(groups) " in *\ admin\ *|*\ sudo\ *)
    if [ -x /usr/bin/sudo ]; then
	cat <<-EOF
	To run a command as administrator (user "root"), use "sudo <command>".
	See "man sudo_root" for details.
	
	EOF
    fi
    esac
fi

# 运行系统中不存在的命令时，command_not_found_handle 函数会被自动调用，提供额外的信息或帮助，而不是简单地输出错误消息
if [ -x /usr/lib/command-not-found -o -x /usr/share/command-not-found/command-not-found ]; then
	function command_not_found_handle {
                if [ -x /usr/lib/command-not-found ]; then
		   /usr/lib/command-not-found -- "$1"
                   return $?
                elif [ -x /usr/share/command-not-found/command-not-found ]; then
		   /usr/share/command-not-found/command-not-found -- "$1"
                   return $?
		else
		   printf "%s: command not found\n" "$1" >&2
		   return 127
		fi
	}
fi
```

