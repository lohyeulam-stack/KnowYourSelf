# Owner 快捷操作说明 v2

## 开始
`按 Bootstrap Prompt v2 开始。当前只做 Discovery，不允许搭建和迁移。每轮只问一个最高价值问题。`

## 查看状态
`/status`

## 修改旧决定
`修改之前关于【主题】的答案。旧答案标记 SUPERSEDED。新答案是：……`

## 暂停追问，先总结
`先不要继续提问。总结：已确认 / OPEN / 冲突 / RECOMMENDATION / 下一 Gate。`

## 架构评审
`进入 ARCHITECTURE_OPTIONS。至少给两个结构不同的方案，不实施。`

## 冻结部分架构
`/freeze 【范围】`

## 只搭 Pilot
`/build-pilot`

## 上下文过重时
`你正在违反 No Recursive Context Boot。停止全文扫描，重新按 Security Domain → Project → Feature → Task 生成最小 Context。`

## 多项目同时被加载时
`违反 Local Detail, Global Summary。项目细节留在项目内，Portfolio 只允许读取 Project Health Snapshot。`

## 长会话时
`生成 SESSION_HANDOVER。Conversation is Ephemeral; State is Persistent。后续从 Handover 继续。`

## Agent 过早开工时
`停止实施。当前 Architecture 尚未 Frozen。回到 Discovery / Review。`
