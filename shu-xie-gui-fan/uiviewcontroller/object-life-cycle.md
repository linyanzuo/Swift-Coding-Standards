# 对象生命周期方法
> 所有与视图控制器相关的生命周期方法，书写在连续区域内，并使用“Mark”进行标注

控制器生命周期的相关方法包括：
* 指定构造方法
* 便捷构造方法
* 所有重写父类的构造方法
* 析构方法

## 书写顺序
> 作为构造对象的入口, 控制器生命周期方法应该尽量写在类的开始位置

如果该类存在类方法, 则控制器生命周期方法写在类方法后面

## 构造方法
> 

## 划分规则
**注释要求**
```
// MARK: - Object Life Cycle
```

**示例代码**
```
// MARK: - Object Life Cycle

/// 指定构造器
public required init?(coder aDecoder: NSCoder) {
    super.init(coder: aDecoder)
    // ... 省略代码 ...
}

/// 便捷构造器
public convenience init(contentSize: CGSize) {
    self.init(nibName: nil, bundle: nil)
    // ... 省略代码 ...
}

/// 重写父类的构造器
public override init(nibName nibNameOrNil: String?, bundle nibBundleOrNil: Bundle?) {
    super.init(nibName: nibNameOrNil, bundle: nibBundleOrNil)
    // ... 省略代码 ...
}

/// 析构方法
deinit {
    // ... 省略代码 ...
}
```
