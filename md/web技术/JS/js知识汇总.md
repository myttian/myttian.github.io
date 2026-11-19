# JS开发工具

[常用JS开发工具](https://blog.51cto.com/u_17389086/14202683?)  

### JS 开发工具的主要类别

- 编辑器与 IDE：VS Code、WebStorm、Sublime Text
- 构建与打包工具：Webpack、Vite、Rollup
- 调试工具：Chrome DevTools、Safari Inspector、Node.js Debugger、WebDebugX
- 测试与质量保障工具：Jest、Mocha、Cypress、Playwright、ESLint、Prettier
- 性能优化工具：Lighthouse、Bundle Analyzer

# 构建工具

## js构建工具

[JavaScript 构建工具](https://blog.csdn.net/Flying_Fish_roe/article/details/144826299)  [JavaScript构建工具](https://www.php.cn/faq/1823024.html) [构建工具与自动化](https://blog.csdn.net/hummhumm/article/details/143156363)   [javascript构建工具](https://www.php.cn/faq/1888767.html)  

[gulp.js - 基于流(stream)的自动化构建工具](https://www.gulpjs.com.cn/)  



JS构建工具主要分两类：任务运行器（Grunt、Gulp）和模块打包器（Webpack、Rollup、Vite、Parcel）。现在新项目最主流的选择是 Vite，老牌大项目多沿用 Webpack，库开发则常用 Rollup。

### 主流工具怎么选

1. Vite：当前最推荐的新项目首选。开发环境基于原生 ES 模块，冷启动和热更新极快，生产构建用 Rollup，Vue/React 项目开箱即用。
2. Webpack：生态最丰富、功能最全，适合大型复杂项目。配置繁琐、启动较慢，但代码分割、懒加载等优化手段成熟。
3. Rollup：专注打包 JS 库/组件库，Tree-shaking 彻底、产物干净体积小，适合发布 npm 包。
4. Parcel：零配置开箱即用，适合小型项目或快速原型，定制性较弱。
5. Gulp：基于流的任务运行器，适合文件压缩、混淆、拷贝等自动化流程，不负责模块打包。
6. Grunt：老牌任务运行器，配置繁琐，新项目基本不再从零使用。

### 核心差异

| 工具    | 适用场景                 | 配置复杂度 | 构建速度 |
| ------- | ------------------------ | ---------- | -------- |
| Vite    | 中大型项目、现代框架开发 | 低         | 极快     |
| Webpack | 大型复杂项目             | 高         | 慢       |
| Rollup  | 库/组件库打包            | 中         | 中       |
| Parcel  | 小型项目、原型           | 极低       | 快       |
| Gulp    | 静态资源处理、任务自动化 | 低         | 快       |

### 选型建议

- 新项目（Vue/React）：直接上 Vite，开发体验提升明显。
- 大型企业项目：Webpack 生态最稳，踩坑资料多。
- 发布 npm 包：Rollup 是标配，产物干净。
- 老项目维护：沿用现有工具，不必强行迁移。

> 补充：Vite 生产构建底层用的就是 Rollup，所以两者不是竞争关系，而是互补。开发用 Vite 的快，打包用 Rollup 的精。

工具选择背后还有不少细节，比如Vite的原生ES模块开发环境如何实现?或者Webpack的代码分割具体怎么配置?