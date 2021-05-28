# 码云代码提交规范

## 代码提交格式

```shell
# type 提交类型
# scope 影响范围，可选
# subject 代码修改描述
type(scope?): subject
```

**冒号后为空格**

## `type` 提交类型

| 类型     | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| build    | 主要目的是修改项目构建系统(例如 glup，webpack，rollup 的配置等)的提交 |
| ci       | 主要目的是修改项目继续集成流程(例如 Travis，Jenkins，GitLab CI，Circle等)的提交 |
| docs     | 文档更新                                                     |
| feat     | 新增功能                                                     |                                                          |
| fix      | bug 修复                                                     |
| perf     | 性能, 体验优化                                               |
| refactor | 重构代码(既没有新增功能，也没有修复 bug)                     |
| test     | 新增测试用例或是更新现有测试                                 |
| revert   | 回滚某个更早之前的提交                                       |
| style    | 不影响程序逻辑的代码修改(修改空白字符，格式缩进，补全缺失的分号等，没有改变代码逻辑) |
| chore    | 不属于以上类型的其他类型                                     |


## `scope` 影响范围

可以是以下几种情况

- `controller` 控制器
- `route` 路由
- `view` 视图
- `model` 模型
- 无 其他

```
fix: 修改xxx bug
```

## `subject` 描述信息

描述信息应完整描述修改的内容



