### `[建议]` 每行代码长度限制
> Swift 每行代码长度应该小于 100 个字符，或者说阅读的时候不应该需要滚动屏幕，在正常的实现范围里可以完整看到代码。

超过100个字符应该换行, 但下列情况例外: 

* 如果是一串有意义的连续文本不需要换行，比如一句注释里的一个很长的 URL。
* `import` 声明。
* 生成的代码。

### `[建议]` 代码换行
> 为了可读性在一些声明里可以把一行过长的代码分成几行

当然断句也要遵循一定的规则：
* 最前面的函数基本名称和泛型的声明不能断开。
* 参数末尾的右括号和返回值的声明不能断开。
* 参数列表可以断开。
* 泛型约束可以断开。

还有一些换行的原则： 
* 可以断开的语句前面要加一个缩进。
* 参数列表如果要断开，那么必须每一个参数单独一行。（只有“全部在一行”和“每个参数一行”这两种形式）
* 如果函数声明的结尾是可以断开的单元，那么函数体的开始左花括号单独一行。

```
public func index<Elements: Collection, Element>(
    of element: Element,
    in collection: Elements
) -> Elements.Index?
where
    Elements.Element == Element,
    Element: Equatable
{  // 注意花括号换行了
    // ... 省略方法体实现 ...
}
```

如果带有 `where` 关键字的泛型约束，那么还有两条规则：
* 如果返回值加上 `where` 后面的声明超过了每行长度的限制，那么从 where 开始换行，where 与原始行在同一级的缩进。
* 如果 `where` 后面的约束整句还是超过了长度的限制，那么每个约束单独换行，并且结尾后带一个换行。

这样的断句样式保证了不同部分的声明可以快速、轻松的被读者通过换行和缩进识别出来，同时在整个文件中保持相同的缩进级别。

```
public func index<Elements: Collection, Element>(
    of element: Element,  
    in collection: Elements
) -> Elements.Index?
where Elements.Element == Element, Element: Equatable 
{
    // ... 省略方法体实现 ...
}
```


