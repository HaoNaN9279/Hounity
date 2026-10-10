# Hounity

基于 GraphView 的 Unity 节点化 HDA 工作流系统。

## 简介

Hounity 在 Unity 编辑器内构建一套**节点化的 HDA 工作流系统**，替代 Houdini Engine for Unity 传统的「一个 HDA = 一个场景 GameObject」用法。它将 HDA 视为工作流图中的一个节点，多个 HDA 节点与其他工具节点通过连线组合，最终产出离线资产（Mesh、Prefab、ScriptableObject 等），而非场景中的实时对象。

底层复用 Houdini Engine Core 作为执行引擎，上层构建节点系统与工作流引擎。

## 核心特性

- **节点化工作流**：基于 Unity GraphView 的数据处理图，支持图序列化、依赖排序与增量执行。
- **HDA 节点**：封装 HDA 资产与参数，映射暴露参数到 Unity 编辑器字段。
- **选择器节点**：资源选择器（单/多资源、命名过滤）与 GameObject 选择器（层级递归、命名、组件字段值）。
- **Mesh 工具节点**：LOD 生成、ShadowProxy 生成、CollisionMesh 生成。
- **预览节点**：离屏渲染 Mesh，支持旋转/缩放/平移。
- **输出节点**：将数据序列化为离线资产。
- **多任务管理器**：Session 池、任务队列、进度与取消。
- **不卡主线程**：异步 Cook + Job System / Burst + 分帧执行。

## 架构分层

```
Editor UI Layer        GraphView 编辑器 / 节点 Inspector / 多任务管理器面板
Workflow Engine Layer  图序列化 / 依赖排序 / 增量 Cook 调度 / 缓存管理
Node System Layer      HDA / 资源选择 / GameObject 选择 / Mesh 工具 / 预览 / 输出
Houdini Bridge Layer   HEU_HoudiniAsset 封装 / 参数映射 / 异步 Cook 管理
Houdini Engine Core    HAPI Session / HDA Cook / 几何输出（外部）
```

## 技术依赖

- Unity 2022.3
- Houdini Engine for Unity 插件（Houdini Engine Core）
- Unity GraphView（`UnityEditor.Experimental.GraphView`）
- Unity Job System / Burst Compiler
- VHACD（凸分解，Native Plugin 或内置）

## 文档

- [设计方案](docs~/设计方案.md)：完整架构与模块设计。
- [开发规划](docs~/开发规划.md)：里程碑、任务分解与验收标准。

## 状态

早期开发阶段。详见[开发规划](docs~/开发规划.md)。

## 许可证

[MIT](LICENSE)
