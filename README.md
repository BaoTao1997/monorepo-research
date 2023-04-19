# monorepo-research

## 背景

调研现有的Monorepo技术方案并写一些基础的Demo，为后续组件库以及相应多包需求作为指导方案。

## Monorepo介绍

Monorepo 是一种项目代码管理方式，指单个仓库中管理多个项目，有助于简化代码共享、版本控制、构建和部署等方面的复杂性，并提供更好的可重用性和协作性。中大型项目，多模块项目，更适合用 MonoRepo 方式管理代码，在开发、协作效率、代码一致性方面都能受益。

## Monorepo问题

1. Q: npm/yarn 安装依赖时，存在依赖提升，某个项目使用的依赖，并没有在其 package.json 中声明，也可以直接使用，这种现象称之为 “幽灵依赖”；随着项目迭代，这个依赖不再被其他项目使用，不再被安装，使用幽灵依赖的项目，会因为无法找到依赖而报错。
A: 可以通过 pnpm/rush 彻底解决这个问题

2. Q: MonoRepo 中每个项目都有自己的 package.json 依赖列表，随着 MonoRepo 中依赖总数的增长，每次 install 时，耗时会较长。
A: 相同版本依赖提升到 Monorepo 根目录下，减少冗余依赖安装；使用 pnpm 按需安装及依赖缓存。增量构建，而非全量构建；也可以将串行构建，优化成并行构建。

## Monorepo方案

### Lerna + Nx

Lerna 优化了多包工作流，解决了**多包依赖**、**发版手动维护版本**等问题，不提供构建、测试等任务，工程能力较弱。

Lerna解决了什么问题

- **代码共享，调试便捷**： 一个依赖包更新，其他依赖此包的包/项目无需安装最新版本，因为 Lerna 自动 Link。
- **安装依赖，减少冗余**：多个包都使用相同版本的依赖包时，Lerna 优先将依赖包安装在根目录。
- **规范版本管理**： Lerna 通过 Git 检测代码变动，自动发版、更新版本号；两种模式管理多个依赖包的版本号。
- **自动生成发版日志**：使用插件，根据 Git Commit 记录，自动生成 ChangeLog。

### pnpm + changesets

### RushStack

## 参考文章

1. [快手数平Monorepo选型](https://juejin.cn/post/7215886869199896637)
2. [Monorepo管理工具选择](https://juejin.cn/post/7146788615032340494)
3. [基于Rush的Monorepo发包实践](https://github.com/worldzhao/blog/issues/12)
4. [大型前端项目管理模式实践](https://mp.weixin.qq.com/s/N0CZABDD0TKTmdljH3y74A)
5. [lerna 还是 pnpm + changesets](https://juejin.cn/post/7220681627977318458)
