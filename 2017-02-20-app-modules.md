# App的模块化

一点浅薄的经验

分出章回、批阅十载

作者：[@nixzhu](https://twitter.com/nixzhu)

---

相对于桌面应用，虽然App运行于小小的手机上，但其开发同样也是一项完整的软件工程。相较于一些日常测试的小Demo，一个成熟的App的代码行数可能会以数十万计。我常常想，要是我能在一开始就“看”到此时这款App的代码结构，定会少走许多弯路。

随着开发的进展，代码逐渐增多，某些代码会显著被其它代码依赖，最后我们甚至可以给它们起个名字，比如叫做某某模块。既然这样叫，那为什么不真的独立出来？

开个分支，增加一个Target，将一些文件放到其中，修复编译错误（加一些public等），再修改此Target暴露给外部的API，让它更好使用。

我的建议是每两周都这么想一想、做一做，目前的代码里有没有可以独立出来的模块？然后花一点时间去把它从源项目中剥离出来。

可能很不幸，你看到这篇文章的时候，你的项目已经很大了，虽然从某些文件的名字看起来它确实应该独立为一个模块了，但并没有人来做这件事，甚至其实其代码对其他部分的依赖还很严重，短时间来看并不容易分离。

那么我们可以换一个思路，这个App的核心是什么？

就我来看，可能有网路层、模型、持久化等。也就是说，有了这些，你可以用它写一个命令行版的App出来。

既然如此，先将这个“核心”剥离出来，它的特征是缺少了它App就不可能工作，且不依赖任何UI的部分。

再之后，分析自己的App，或者有意识地持续分离不应该互相依赖的部分，最后渐渐独立出各种模块来，把它们变成Framework。

以上总结起来却很简短：编写代码时有意识地注意“复用”和“重构”。每次你要从其他文件里拷贝代码的时候都应该思考一下，这段代码适合变成一个函数吗？应该放在Extension里还是写一个类封装一下？每次修改一个函数的时候，就观察它是否太长？是否不易读懂？是否参数过多？甚至是否命名不合适？

就如初生的婴儿，你愿意它健康合理地成长还是变成一团谁也解不开地乱麻？

有错误自然要修复，有警告也要积极处理。