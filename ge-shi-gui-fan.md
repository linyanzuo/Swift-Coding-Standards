### 格式规范说明

**示例格式**

* `[执行要求]` 格式描述

**说明**
* [强制] 表示该规则要求强制执行, 严格遵守该规则
* [建议] 表示该规则仅供参考, 尽量按规则命名, 但不要求强制执行
* 格式描述 描述本规则指定的格式名称

---

### `[强制]` 缩进符
使用4个空格表示一个缩进, 即XCode中的默认一个Tab键

```
required init?(coder aDecoder: NSCoder) {
    super.init(coder: aDecoder)
    // ... 省略 ... 
}
```

### `[建议]` 括号
* 非空的 block 花括号默认使用`K&R`样式，即“左大括号`{`不要单独占据一行, 放置在上一行的末尾, 中间用一个空格隔开”
    ```
    // ✅
    while (x == y) {
        something()
        somethingelse()
    }
    ```
    
* 最顶级的 if、guard、while、switch 的条件不使用括号
    ```
    // ✅, 不使用括号
    if x == 0 {
      print("x is zero")
    }
    
    // ✅, 有优先级考虑，才使用括号
    if (x == 0 || y == 1) && z == 2 {
      print("...")
    }
    
    // ❌，条件的最外层不需要使用括号
    if (x == 0) {
      print("x is zero")
    }
    
    // ✅, 有多条件需求时, 才使用
    if ((x == 0 || y == 1) && z == 2) {
      print("...")
    }
    ```

下列特殊情情况例外:
* 通常情况下, 左花括号 `{` 后都是一个换行，除非:
    1. 后面要声明闭包的参数，改为在 `in` 关键字后面换行。
    1. 符合[每行只声明一件事]()的情况，忽略换行，把内容写在一行里。
    1. 如果是空的 `block`, 直接声明为 `{ } `
* 右花括号 `}` 后是一个换行，除非:
    1. 如果右花括号后面跟的是 `else`，可考虑写成 `} else {` 进行衔接
    
### `[强制]` 分号
> 无论是终止或者隔开声明都不会使用分号。也就是说分号只可能出现在文本中。

```
func printSum(_ a: Int, _ b: Int) {
    // ❌，禁止在代码中出现分号
    let sum = a + b;
    
    // ❌，只能在文本中使用分号
    print(sum + " end;")
}
```

### `[建议]` 空格
> 除了语言或者其他样式的要求，文字和注释之外, 一个 `Unicode` 空格也只出现在以下地方:

* 条件关键字后面和跟着的括号之间
* 在任何二元或三元运算符的两边
    ```
    // ✅
    if (x == 0 && y == 0) || z == 0 {
         // ... 省略 ...
    }
    
    // ❌，条件关键字`if`后面需要添加括号
    if(x == 0 && y == 0) || z == 0 {
        // ... 省略 ...
    }
    
    // ❌，运行符的两边需要添加括号
    if (x==0 && y==0) || z==0 {
        // ... 省略 ...
    }    
    ```
    
* 使用于赋值，初始化变量、属性，默认参数的等号两边。
    ```
    // ✅
    var x = 5

    // ✅
    func sum(_ numbers: [Int], initialValue: Int = 0) {
        // ... 省略 ...
    }

    // ❌，初始化变量或赋值的等号两边需要添加空格
    var x=5

    // ❌，默认参数的等号两边添加空格
    func sum(_ numbers: [Int], initialValue: Int=0) {
        // ... 省略 ...
    }
    ```
    
* 如果闭包中的代码在同一行，左花括号的前面、后面，右花括号的前面有空格。
    ```
    let nonNegativeCubes = numbers.map { $0 * $0 * $0 }.filter { $0 >= 0 }
    
    // ❌，同一行时花括号前后有空格
    let nonNegativeCubes = numbers.map{$0 * $0 * $0}.filter{$0 >= 0}
    ```
    
* 在协议中表示合成类型的 & 两边。
    ```
    // ✅
    func sayHappyBirthday(to person: NameProviding & AgeProviding) {
        // ... 省略 ...
    }
    
    // ❌，& 前后需要添加空格
    func sayHappyBirthday(to person: NameProviding&AgeProviding) {
        // ... 省略 ...
    }
    ```
    
* 表示返回值的两边。
    ```
    // ✅
    func sum(_ numbers: [Int]) -> Int {
      // ... 省略 ...
    }
    
    // ❌
    func sum(_ numbers: [Int])->Int {
      // ... 省略 ...
    }
    ```
    
* 参数列表、数组、tuple、字典里的逗号后面有一个空格
    ```
    // ✅
    let numbers = [1, 2, 3]
    
    // ❌, 逗号后面缺少空格
    let numbers = [1,2,3]
    // ❌, 内容与逗号之间不需要空格
    let numbers = [1 ,2 ,3]
    // ❌
    let numbers = [1 , 2 , 3]    
    ```
    
* 冒号的后面添加一个空格
    ```
    // ✅, 类型声明
    struct HashTable: Collection {
      // ...
    }
    
    struct AnyEquatable<Wrapped: Equatable>: Equatable {
      // ...
    }
    
    // ✅, 参数标签
    let tuple: (x: Int, y: Int)
    
    func sum(_ numbers: [Int]) {
      // ...
    }
    
    // ✅, 变量声明
    let number: Int = 5
    
    // ✅, 字典声明
    var nameAgeMap: [String: Int] = []
    
    // ✅, 字典字面量
    let nameAgeMap = ["Ed": 40, "Timmy": 9]
    ```
    
* 代码后的注释符号 `//` 与代码间有两个空格距离
    ```
    // ✅
    let initialFactor = 2  // Warm up the modulator.
    ```
* 表示字典、数组字面量的中括号外面有一个空格, 里面不需要
    ```
    // ✅
    let numbers = [1, 2, 3]
    // ❌， 字典、数组字面量的中括号里面不需要空格
    let numbers = [ 1, 2, 3 ]
    ```

> 不使用空格的例外情况下如：

* 表示区域范围的 `..<` 和 `…` 两边没有空格。
    ```
    // ✅
    for number in 1...5 {
        // ... 省略 ...
    }
    
    // ❌，表示区域范围的两边不需要添加空格
    let substring = string[index..<string.endIndex]
    for number in 1 ... 5 {
        // ...
    }
    ```
    
### `[建议]` 每行代码只声明一件事
> 每行最多只声明一件事，每行结尾用换行分隔。除非结尾跟的是一个总共只有一行声明的闭包。

```
guard let value = value else { return 0 }

let squares = numbers.map { $0 * $0 }

var someProperty: Int { return otherObject.somethingElse() }

switch someEnum {
case .first: return 5
case .second: return 10
case .third: return 20
}

var someProperty: Int {
  get { return otherObject.property }
  set { otherObject.property = newValue }
}

required init?(coder aDecoder: NSCoder) { fatalError("no coder") }
```
如果闭包是提前返回一个值，写在一行里可读性就会好一些。如果是一个正常的操作，可以视情况是否写在一行里

### `[建议]` 禁止变量、属性水平对齐
> 除非是在写明显的表格数据，否则水平对齐是明确禁止的。
> 虽然略对齐会损害可读性，但引入水平对齐后，如果添加一个新的成员可能会需要其他成员再对齐一次，这给维护增加了负担。

```
// ✅
struct DataPoint {
  var value: Int
  var primaryColor: UIColor
}

// ❌，禁止水平对齐
struct DataPoint {
  var value:        Int
  var primaryColor: UIColor
}
```





















