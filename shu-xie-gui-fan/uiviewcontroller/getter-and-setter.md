# 属性的Get、Set方法
> 控制器内所有的Get, Set方法，都书写在连续区域内，并使用`Mark`一级标注

> `[建议]`为避免影响代码逻辑的阅读，将所有懒加载方法放置在代码的最后

## 划分规则

**注释要求**
```
// Mark: - Getter & Setter
```

**示例代码**
```
// MARK: - Getter & Setter

private lazy var vipImgView: UIImageView = { 
    /// ...省略代码...
}

private lazy var cardView: WHomeCardHeaderView = {
    /// ...省略代码...
}
```

## 根视图的直接子视图

* 所有在控制器内创建的视图，都使用懒加载的方式声明并进行样式配置
* 控制器最迟在`setupSubview`方法中更新约束时, 会实例化这些子视图
* 若命名的语义无法清晰描述子视图，则添加`/// 子视图描述`注释
```
/// 封面图
private(set) lazy var coverImgView: MoeImageView = {
    // ... 省略代码 ...
}()
```

