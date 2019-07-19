# 代理方法
> 控制器内所有的代理方法，都书写在连续区域内，并使用`Mark`一级标注

* 不同协议的代理方法，使用`Mark`二级标注，注释内容为协议名
* 如果仅有一个协议的代理方法，可以省略`Mark`一级标注
    * 如`// Mark: -- UITableViewDatasource`
* 有关联的代理方法，可以合并写在同个`Mark`二级标注内，使用` & `进行隔开
    * 如`// Mark: -- UITableViewDatasource & UITableViewDelegate`
    
## 划分规则

**注释要求**
```
// MARK: - Delegate Methods
```

**示例代码**
```
// Mark: - Delegate Methods

// MARK: -- UITableViewDelegate & UITableViewDatasource

override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    // ... 省略代码 ...
}

override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    // ... 省略代码 ...
}

// MARK: -- MoeSearchResultProtocal

var datasources: [Any]? {
    didSet {
        // ... 省略代码 ...
    }
}
```

## 使用 Extension 书写代理方法
> 对于代码方法较多的协议, 如`UITableViewDelegate & UITableViewDatasources`, 可以使用`Extension`来独立书写代理方法的实现

* 若`Extension`写在独立文件, 则命名应该使用`类名+协议描述`的形式
    * 如为首页`HomeVC`扩展`TableView`相关的协议方法, 推荐命名为`HomeVC+TableView.swift`
    * 如为首页`HomeVC`扩展`UIGestureRecognizer`协议方法, 推荐命名为`HomeVC+Gesture.swift`
* 若`Extension`在类文件中继教写, 则建议使用两个换行与类代码隔开


