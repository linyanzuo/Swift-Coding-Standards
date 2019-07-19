### 函数声明
参照[代码长度与换行](/swift-style-guide/ge-shi-gui-fan/dai-ma-chang-du-yu-huan-xing.md)中“代码换行”的建议，可以得到如下的结构

1. `修饰符 func 函数名(` `参数列表` `)` {
1. `修饰符 func 函数名(` `参数列表` `) ->` `返回值类型` {
1. `修饰符 func 函数名<` `泛型参数` `>(` `参数列表` `) throws ->` `返回值类型` {
1. `修饰符 func 函数名<` `泛型参数` `>(` `参数列表` `) throws ->` `返回值类型` `where` `泛型约束条件` {

其中： 
* “参数列表”与“泛型约束条件”可以拆分成多行
* 大部分函数都没有泛型约束条件，此时右括号、返回值、左花括号应尽量放置在一行

函数的声明根据代码换行的要求进行拆分换行， 示例如下：

```
✅
public static func makeLabel(
    appear: MoeViewAppear,
    toView: UIView,
    _ closure: appearClosure?
) -> MoeLabel {
    return internalMakeLabel(appear: appear, toView: toView, closure)
}
```

### 协议声明
在协议中声明的函数，右括号可以与最终参数放在同一行上，也可以单独列一行。

> `[建议]` 右括号放在同一行, 根据实际情况考虑用换行隔开下一行代码

```
✅
public protocol ContrivedExampleDelegate {
    func contrivedExample(_ contrivedExample: ContrivedExample,
                          willDoSomethingTo someValue: SomeValue)
}
​
public protocol ContrivedExampleDelegate {
    func contrivedExample(
        _ contrivedExample: ContrivedExample,
        willDoSomethingTo someValue: SomeValue
    )
}
```

如果声明中参数、约束、返回值的某个元素非常复杂或者有多层嵌套（比如参数是一个闭包，元组），可参照[代码换行](/swift-style-guide/ge-shi-gui-fan/dai-ma-chang-du-yu-huan-xing.md)的建议进行折分

> `[建议]` 元素类型非常复杂，建议使用 `typealias` 取一个别名来简化声明的复杂度

```
public func performanceTrackingIndex<Elements: Collection, Element>(
    of element: Element,
    in collection: Elements
) -> (                 // 返回值是一个复杂的 tuple
    Element.Index?,
    PerformanceTrackingIndexStatistics.Timings,
    PerformanceTrackingIndexStatistics.SpaceUsed
) {
      // ... 省略方法体实现 ...
}
```

### 类型与扩展的声明
下面的例子适用于 `class`，`struct`，`enum`，`extension`，`protocol`

声明的结构拆分如下： 

1. `class 类名` {
1. `class 类名:` `父类和协议` {
1. `class 类名<` `泛型参数` `>:` `父类和协议` {
1. `class 类名<` `泛型参数` `>:` `父类和协议` `where` `泛型约束条件` {

参考例子如下： 

```
// 继承的父类与遵守的协议太多，一行内容无法放下时，拆分成多行，每行一个
class MyClass:
    MySuperclass,
    MyProtocol,
    SomeoneElsesProtocol,
    SomeFrameworkProtocol
{
    // ... 省略方法体实现 ...
}

// 有泛型参数时， 跟随类名后面不换行
class MyContainer<Element>:
    MyContainerSuperclass,
    MyContainerProtocol,
    SomeoneElsesContainerProtocol,
    SomeFrameworkContainerProtocol
{
    // ... 省略方法体实现 ...
}

// where的泛型约束条件，一行装得下时不换行
class MyContainer<BaseCollection>:
    MyContainerSuperclass,
    MyContainerProtocol,
    SomeoneElsesContainerProtocol,
    SomeFrameworkContainerProtocol
where BaseCollection: Collection {
    // ... 省略方法体实现 ...
}

// where的泛型约束条件，超过一行，换行时每个条件单独一行
class MyContainer<BaseCollection>:
    MyContainerSuperclass,
    MyContainerProtocol,
    SomeoneElsesContainerProtocol,
    SomeFrameworkContainerProtocol
where
    BaseCollection: Collection,
    BaseCollection.Element: Equatable,
    BaseCollection.Element: SomeOtherProtocolOnlyUsedToForceLineWrapping
{
    // ... 省略方法体实现 ...
}
```

### 函数调用
当函数断句换行时，每一个参数都声明在独立的一行中，跟原始行有 2 个空格缩进。
和函数声明一样，函数调用结尾的右括号（没有尾闭包）既可以在参数行的末尾，也可以单独起一行。

> `[建议]` 右括号放在同一行, 根据实际情况考虑用换行隔开下一行代码

参考例子如下： 

```
let index = index(
    of: veryLongElementVariableName,
    in: aCollectionOfElementsThatAlsoHappensToHaveALongName)
​
let index = index(
    of: veryLongElementVariableName,
    in: aCollectionOfElementsThatAlsoHappensToHaveALongName
)
```

如果函数调用时有尾闭包且需要换行时（一行装不下），则闭包参数必须单独一行且使用括号括起来，以便与闭包的方法体区分开来

参考例子如下： 

```
someAsynchronousAction.execute(withDelay: howManySeconds, context: actionContext) {
    (context, completion) in
    doSomething(withContext: context)
    completion()
}
```

### 控制流声明
> `[强制]` 控制流不需要断句换行时，结尾的花括号不需要换行

当一个控制流的声明需要断句换行（比如 if、guard、 while、 for）时； 

* 继续的下一行和前一行保持一样的缩进(换行)
    * 如果语法上是嵌套，前面加2个空格缩进
* 结尾的花括号可以接着末尾或单独起一行
    > `[建议]` 控制流语句若断句换行，结尾的花括号应该单独一行，代码结构更清晰
* 对于 `guard`，不管是接着当前行末尾还是单独另起一行，都要求 `else` 与 `{` 必须写在一起

参考例子如下： 

```
// 控制流需要换行时，结尾的花括号建议另起一行
if aBooleanValueReturnedByAVeryLongOptionalThing() &&
    aDifferentBooleanValueReturnedByAVeryLongOptionalThing() &&
    yetAnotherBooleanValueThatContributesToTheWrapping() 
{
    doSomething()
}

// 控制流需要换行时，结尾的花括号建议另起一行
if let value = aValueReturnedByAVeryLongOptionalThing(),
   let value2 = aDifferentValueReturnedByAVeryLongOptionalThingThatForcesTheBraceToBeWrapped()
{
    doSomething()
}

// guard需要换行时，`else {` 建议换行
guard let value = aValueReturnedByAVeryLongOptionalThing(),
      let value2 = aDifferentValueReturnedByAVeryLongOptionalThing()
else {
    doSomething()
}

// 控制流需要换行时，结尾的花括号建议另起一行
for element in collection
    where element.happensToHaveAVeryLongPropertyNameThatYouNeedToCheck 
{
    doSomething()
}
```
