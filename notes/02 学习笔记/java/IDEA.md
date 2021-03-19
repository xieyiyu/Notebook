## Idea文件夹类型
1. Source roots：通过将文件夹指定为这种类别，来告诉IntelliJ IDEA，这个文件夹和它的子文件夹中包含源码，在构建工程时，需要作为一部分被编译进去。
2. Test source roots：这个类型的文件夹与sources root类似，都是用于存放源码，不过是测试的源码（比如单元测试）。test sources root 文件夹可以帮助你将测试代码和产品代码分离开。通常sources root和test sources root的编译结果被放在不同的文件夹中。
3. Resource roots： 存放你的应用中需要用到的资源文件（如：图片、xml或者properties配置文件等）
4. Test resource roots：存放和test resources关联的资源文件
5. Excluded roots：几乎被忽略的。为排除的文件夹中的文件提供了非常有限的编码帮助。
