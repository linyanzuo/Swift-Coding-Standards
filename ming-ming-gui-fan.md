## 命名规范说明

**示例格式**

* `[执行要求]` 命名描述

**说明**
* [强制] 表示该规则要求强制执行, 严格遵守该规则
* [建议] 表示该规则仅供参考, 尽量按规则命名, 但不要求强制执行
* 命名描述 描述本规则指定的命名规范

---

### `[建议]` 建议拒绝的命名

* 建议拒绝使用 `汉语拼音` 来命名, 如 
    ```
    let shenmegui = "什么鬼"
    let ren = Person()

    func jiafa(a: Int, b: Int) -> Int {
        return a + b
    } 

    class qian {
        // ...省略代码...
    }
    ```

* 建议拒绝使用 `第N个` 的命名方式, 如
    ```
    let model1 = new Model("default")
    let model2 = new Model("lightContent")
    let model3 = new Model("none")

    // 推荐的命名方式
    let defaultModel = new Model("default")
    ```

---

### `[建议]` 前缀
* Swift中类别(类，结构体)在编译时会把模块设置为默认的命名空间, 所以不用为了区分类别而添加前缀
* 为了和引用的第三方库作区分, 建议使用前缀, 以便规范的识别业务代码
* 封装组件, 静态库, 动态库, Pod时, 不要使用前缀

### `[强制]` 文件名
所有swift源文件都使用`.swift`扩展名, 通常使用源文件中的主体来命名
如果是扩展现有的类型, 则在现有类型命名上, 使用 `+` 号带上扩展内容

* 如果是单一类型, 如描述汽车的类, 那么文件名为 `Car.swift`
* 如果是扩展 `Car` , 实现了 `UIGestureRecognizer` 协议, 文件为 `Car+UIGestureRecognizer.swift` , 或者是简要描述 `Car + Gesture.swift`
* 如果是扩展 `Car` 增加了一些关于驾驶的扩展方法, 可以将主要方法描述来命名, 如 `Car+Driver.swift`
* 如果文件里的声明不止一个类型, 如包含多个类, 可以描述这些声明的作用或场景, 比如`Math.swift`

### `[强制]` 变量, 常量的命名
变量(`var`)和函数(`func`)使用小驼峰命名规则, 第一个单词小写，其他单词首字母大写

> 当命名里出现缩写词时，缩写词要么全部大写，要么全部小写, 建议全部大写

```
// username 是一个单词, 不用写成 userName
var username = "zed"

// name是第二个单词, 首字母大写
let productName = "Swift Style Guide"

// URL缩写词, 建议全部大写
let fileURL = "/Users/zed/localized.sh"
```

### `[建议]` 静态常量命名
静态常量命名, 根据需求采取两种规则
* `k + 大驼峰`, 如: kButtonHeight, kReuseID
* `小驼峰`, 如: UIColor.themeColor

```
class MyClassName {
    // 类内部使用的静态常量, 推荐使用`k + 大驼峰`规则
    static let kSomeConstantHeight: CGFloat = 80.0
    
    // 类公开使用的静态常量, 推荐语义命名, `小驼峰`规则
    public static let themeColor = UIColor.redColor()
    
    // 声明单例的静态常量, 推荐使用`shared`命名
    static let shared = MyClassName()
    /* ... */
}
```

### 函数(方法)的命名
函数名使用小驼峰命名规则, 第一个单词小写，其他单词首字母大写
当函数的第一个参数构成整个语句的介词时（如，at, by, for, in, to, with 等），为第一个参数添加介词参数标签

```
// 使用小驼峰命名
private static func statusHandler(errorCode: Int, errorMessage: String,  data: Any?) {
    // ... 省略代码 ...
}

// 第一个参数添加介词参数标签, 语义清晰
func login(with username: String, password: String) {
    // ... 省略代码 ...
}
```

### `[强制]` 结构体, 枚举, 类的命名
类型(`Struct`, `Enum`, `Class`)使用大驼峰命名规则, 第一个单词大写，其他单词首字母也大写

> 当命名里出现缩写词时，缩写词要么全部大写，要么全部小写, 建议全部大写

```
// 枚举类型使用大驼峰
public enum HTTPMethod: String {
    // 枚举值(属性)使用小驼峰
    case get     = "GET"
    case post    = "POST"
}

// 结构体类型使用大驼峰
public struct HomeAPI {
    /// 资金账户
    public static let account: MoeURL = ("\(apiHost)/account", .get)
    
    /// 配置信息
    public static let config: MoeURL = ("\(apiHost)/config/investment", .get)
}
```

### `[强制]` Bool 类型命名
布尔类型命名时, 使用`is`作为前缀

```
var isLoading: Bool = false
```

### `[建议]` Array, Dictionary 类型命名
数组或字典类型命名时, 名称要尽量能体现出"多个"的语义, 如复数形式的词汇, 或以类似"some", "many"等开头

> 内容较多时, 需要多行显示, `[` 和 `]` 单独占据一行, 类似于方法体的括号

```
// 多行时要换行显示
let records: [Record] = [
    Record(title: "First", subtitle: "")
    Record(title: "Second", subtitle: "")
    Record(title: "Third", subtitle: "")
]

let someInfo: [String: String] = [
    "title" : "First", 
    "subtitle" : "Null"
]

// 一行放得下
let someRecord: [Record] = [Record(title: "First"), Record(title: "First")]
let infos: [String: String] = ["title" : "First", "subtitle" : "Null"]
```



