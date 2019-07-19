# 网络请求
> 控制器内所有的网络请求方法，都书写在连续区域内，并使用`Mark`一级标注

## 划分规则

**注释要求**
```
// MARK: - Delegate Methods
```

**示例代码**

```
// MARK: - Delegate Methods

private func requestAccount() {
    // ...省略代码...
}

private func requestConfig() {
    // ...省略代码...
}
```

## 命名建议

网络请求的方法, 推荐以`request + 请求描述`形式命名
* 如: 请求用户账号信息, 命名为 `requestAccount()`
* 如: 请求交易记录信息, 命名为 `requestTransactionRecord`





