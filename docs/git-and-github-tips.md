# Git 和 Github 小技巧

## 如何拷贝某个项目的指定目录到本地仓库？

作为Copy攻城狮，要把Copy玩到极致，这不，本仓库想引入自动化测试，但参考React Native采用circlecli，需要配置一大堆文件，如各种脚本，一个一个拷贝又不方便，怎么快捷拷贝呢？请看：

- 确保本机有安装svn（需要用到svn checkout）
- 确定要拷贝的目录，如：
    我想拷贝`facebook/react-native/scripts`这个目录，它的master分支地址是：https://github.com/facebook/react-native/tree/master/scripts  。 
    只需将地址中的 `/tree/master` 替换为 `/trunk` 然后执行 `svn checkout` 命令

- 在需要的目录执行拷贝指令

```bash
svn  checkout ttps://github.com/facebook/react-native/trunk/scripts 

```

如果想拷贝分支下的目录怎么操作呢？只需要将 /trunk/ 换成 /branches/对应分支名称/ 就行了。
比如我想拷贝`0.63-stable` 这个分支的`scripts`目录，它的访问地址是：https://github.com/facebook/react-native/tree/0.63-stable/scripts。 
对应的拷贝地址就是：https://github.com/facebook/react-native/branches/0.63-stable/scripts

您Get到了吗？