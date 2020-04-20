---
toc:
  depth_from: 2
  depth_to: 4
  ordered: false
---

# Markdown Preview Enhanced

[TOC]

参考[MPE官方网站](https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/)

## 优先介绍

优先介绍下面三个功能，看到有三个这么好的扩展就忍不住安装MPE扩展了

### 目录列表（TOC）

参考[MPE官方介绍](https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/toc)

Markdown Preview Enhanced 支持你在 markdown 文件中创建目录，效果就像本教程的目录一样。
基本格式，通过编写 [front-matter](https://jekyllrb.com/docs/front-matter/) 来进行设置：

```markdown
---
  depth_from: 2
  depth_to: 3
  ordered: false
---
```

更详细的用法以后再学！

### 导入外部文件 import

参考[MPE官方介绍](https://shd101wyy.github.io/markdown-preview-enhanced/#/zh-cn/file-imports)

`import`支持导入多种类型的文件，若和本教程一样导入的是markdown文件将会被分析处理然后被引用。支持导入特定行数，如`{line_begin=11}`表示从import指定文件的第11行开始导入，同理`{line_end=-4}`就表示...。

```markdown
    @import '你的文件' {line_begin=11}
```

更详细的用法以后再学！

### 文档导出

我们写好markdown文档预览时是像word一样的有格式的文档，可是我们要怎么样把预览的效果发给别人呢？这就是文档导出功能了。在markdown预览窗口`Preview XXX.md`中（需要你安装Markdown Preview Enhanced插件，并打开其预览窗口，具体参见下一小节的最后一段）右键即可看到好几个导出菜单，这里我们只介绍导出为HTML和PDF。

1. HTML》HTML(offline)，选择这个选项如果你要离线使用这个 html 文件
2. Chrome(Puppeteer)》PDF，导出为PDF
3. eBook》PDF，也可以用这个导出为PDF

导出PDF的多个菜单可以任选其一，

更详细的用法以后再学！

## MPE插件安装

本教程我们需要安装的程序和插件

* vs code最左边的侧边栏第5个图标即是vs code扩展商店，所有vs code扩展插件都可以在这里搜索安装。
* 安装vs code插件`Markdown Preview Enhanced`
* 安装vs code插件`PlantUML`
* 安装 [graphviz](http://www.graphviz.org/download/)
graphviz 是个开源的图片渲染库。安装了这个库才能在 Windows 下实现把 PlantUML 脚本转换为图片。
* 安装jdk1.8或以上，这也是vs code的java开发插件`Java Language Support`支持的最低版本。安装多个版本的jdk不会冲突，所以若你电脑安装了jdk1.6，若使用Eclipse等java开发IDE，可以在IDE中指定工作区的jdk版本如jdk1.6。

安装好插件后，我们打开本教程中的文件："markdown tutorial.md"，即可查看完整的教程，打开文件后右键选择"Markdown Preview Enhanced: Open Preview to the Side"可以看到使用Markdown Preview Enhanced预览的效果。
