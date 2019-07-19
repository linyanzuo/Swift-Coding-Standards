# 事件响应
> 控制器内所有的事件响应方法，都书写在连续区域内，并使用`Mark`一级标注

## 划分规则

**注释要求**
```
// Mark: - Event Response
```

**示例代码**

```
// Mark: - Event Response

@objc private func helpBtnAction(_ btn: UIButton) {
    // ...省略代码...
}

@objc private func submitBtnAction(_ btn: UIButton) {
    // ...省略代码...
}
```

## 命名建议

* 通过`Target-Action`方式添加的事件, 推荐以`控件 + Action`形式命名
    * 如帮助按钮, 命名为`helpBtn`, 则响应事件命名为`helpBtnAction`
* 通过手势添加的事件, 推荐以`控件名 + 手势名 + Action`形式命名
    * 如添加了点击手势的内容标签, 命名为`contentLabel`, 则响应事件命名为`contentLabelTapAction`
