在 vscode 中使用 leetcode，莫名的出现了让我设置了快捷键的地方，我现在也重现不了。当时随便输入了一个 `f`，结果怎么删也删不掉，就直接关掉了。

后面在编码的时候，每次输入 `f` 都会定位到 leetcode 插件中，并且搜索 `f`。真的头大。

当我把 leetcode 插件卸载后，再输入 `f`，报错 `command 'leetCodeExplorer.focus' not found`。

**直接解决办法：**

找到 `C:\Users\Administrator\AppData\Roaming\Code\User\keybindings.json`，发现里面确实有 `leetCodeExplorer.focus`，直接把他删掉就好了。