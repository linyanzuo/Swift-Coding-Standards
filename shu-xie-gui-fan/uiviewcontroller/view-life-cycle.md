# 视图生命周期方法
> 所有与与控制器的根视图相关的生命周期方法，书写在连续区域内，并使用“Mark”进行标注

控制器的根视图的相关生命周期方法包括：
* `func loadView()`
* `func viewDidLoad()`
* `func viewWillAppear(Bool)`
* `func viewDidAppear(Bool)`
* `func viewWillDisappear(Bool)`
* `func viewDidDisappear(Bool)`
* `func viewWillLayoutSubviews()`
* `func viewDidLayoutSubviews()`

## 划分规则
**注释要求**
```
// MARK: - View Life Cycle
```

**示例代码**
```
// MARK: View Life Cycle

override func loadView() {
    // ... 省略代码 ...
}

override func viewDidLoad() {
    super.viewDidLoad()
    // ... 省略代码 ...
}
```

## 统一命名

#### 导航相关的初始化方法
```
func setupNavigation() {}
```

该方法在`viewDidLoad`中被执行, 子类重写该方法, 完成控制器中"导航相关的初始化"工作

* `navigationItem`的配置， 如标题, 返回按钮, 左右两侧按钮
* 导航栏颜色配置, 如前景色, 背景色
* 自定义导航栏配置, 如自定义背景, 上划颜色渐变效果, 上划导航栏消失效果等

> `setupNavigation()`方法, 也书写在`View Life Cycle`区域内

#### 根视图的直接子视图的初始化方法
```
func setupSubview() {}
```

该方法在`viewDidLoad`中被执行, 子类重写该方法, 实现控制器中"根视图", 以及"根视图的直接子视图"的初始化工作.
理论上控制器只负责根视图的初始化工作, 建议由根视图类自行处理子视图的相关初始化

* 通过IB方式关联的控件, 都在本方法中完成额外的样式配置工作, 如更新字体颜色, 标题内容等
* 若视图不复杂时, 可以在控制器中完成对根视图的直接子视图的初始化工作, 建议使用懒加载方式加载子视图,
并在该方法的最后位置为子视图添加约束
* 禁止在控制器中进行根视图的孙级子视图的初始化工作, 复杂子视图代码应抽取, 在独立的视图类中完成

> `setupSubview()`方法, 也书写在`View Life Cycle`区域内






