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
> 对于外部调用者而言, 实例化对象时所需要的操作应当尽量简化

1. 封装相应的`构造方法`和`创建对象实例的类方法`

*示例:*
        调用者需要了解"用户反馈"控制器所处的`Storyboard`文件及绑定的`StoryboardID`, 增加了额外的使用成本
```
let feedbackVC = UIStoryboard(name: "Feedback", bundle: nil).instantiateViewController(withIdentifier: "FeedbackViewController")
```

*建议做法:*
        将使用`Storyboard`实例化对象的方法, 封装成类方法, 调用者只需知道"用户反馈"控制器通过`Storyboard`加载, 并不需要掌握关联的信息
```
class FeedbackVC: UIViewController
    class func storyboardInstance() -> FeedbackVC? {
        return UIStoryboard(name: "Main", bundle: nil).instantiateViewController(withIdentifier: NSStringFromClass(self.classForCoder())) as? FeedbackVC
    }
}
```

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
