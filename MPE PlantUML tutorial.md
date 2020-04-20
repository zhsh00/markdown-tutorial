---
toc:
  depth_from: 2
  depth_to: 4
  ordered: false
---

# PlantUML

[TOC]

## 什么是 PlantUML

[PlantUML](https://plantuml.com/zh/commons) 是一个画图脚本语言，用它可以快速地画出：

* 时序图
* 流程图
* 用例图
* 状态图
* 组件图

## 软件安装

PlantUML应该可以单独使用，但是我是在VS Code中使用他，且是使用Markdown Preview Enhanced扩展来预览渲染效果。

* 安装VS Code插件Markdown Preview Enhanced和PlantUML插件
* 需要java支持，即要安装jdk
* 安装 [graphviz](http://www.graphviz.org/download/)
graphviz 是个开源的图片渲染库。安装了这个库才能在 Windows 下实现把 PlantUML 脚本转换为图片。

## java类图示例

```plantuml
Room o- Student
Room *-- Chair
```

```plantuml
Student -o Room
Chair --* Room
```

```plantuml
foo -left-> dummyLeft
foo -right-> dummyRight
foo -up-> dummyUp
foo -down-> dummyDown
```

```plantuml
class Student {
  Name
}
Student "0..*" - "1..*" Course
(Student, Course) .. Enrollment

class Enrollment {
  drop()
  cancel()
}
```

```plantuml
class Student {
  Name
}
Student "0..*" -- "1..*" Course
(Student, Course) . Enrollment

class Enrollment {
  drop()
  cancel()
}
```

```plantuml
' Split into 4 pages
page 2x2
skinparam pageMargin 10
skinparam pageExternalColor gray
skinparam pageBorderColor black

class BaseClass

namespace net.dummy #DDDDDD {
    .BaseClass <|-- Person
    Meeting o-- Person

    .BaseClass <|- Meeting

}

namespace net.foo {
  net.dummy.Person  <|- Person
  .BaseClass <|-- Person

  net.dummy.Meeting o-- Person
}

BaseClass <|-- net.unused.Person
```

## 时序图示例

```plantuml
title 时序图

== 鉴权阶段 ==

Alice -> Bob: 请求
Bob -> Alice: 应答

== 数据上传 ==

Alice -> Bob: 上传数据
note left: 这是显示在左边的备注

Bob --> Canny: 转交数据
... 不超过 5 秒钟 ...
Canny --> Bob: 状态返回
note right: 这是显示在右边的备注

Bob -> Alice: 状态返回

== 状态显示 ==

Alice -> Alice: 给自己发消息
```

```plantuml :file ./img/plantuml-quickstart-s1.png
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response

Alice -> Bob: Another atuhentication Request
Alice <-- Bob: Another authentication Response
```

TIPS：

* 使用 title 来指定标题
* '->' 和 '-->' 来指示线条的形式
* 在每个时序后面加冒号 : 来添加注释
* 使用 note 来显示备注，备注可以指定显示在左边或右边
* 使用 == xxx == 来分隔时序图
* 使用 ... 来表示延迟省略号
* 节点可以给自己发送消息，方法是发送方和接收方使用同一个主体即可

## 用例图示例

```plantuml
title 用例图
left to right direction
actor 消费者
actor 销售员
rectangle 买单 {
消费者 -- (买单)
(买单) .> (付款) : include
(帮助) .> (买单) : extends
(买单) -- 销售员
}
```

```plantuml :file ./img/plantuml-quickstart-s2.png
actor Foo1
boundary Foo2
control Foo3
entity Foo4
database Foo5
Foo1 -> Foo2 : To boundary
Foo1 -> Foo3 : To control
Foo1 -> Foo4 : To entity
Foo1 -> Foo5 : To database
```

TIPS：

* 用例图是指由参与者（Actor）、用例（Use Case）以及它们之间的关系构成的用于描述系统功能的静态视图
* [百度百科](https://baike.baidu.com/item/%E7%94%A8%E4%BE%8B%E5%9B%BE)上有简易的入门资料，其中用例之间的关系 (include, extends) 是关键
* 使用 actor 来定义参与者
* 使用括号 (xxx) 来表示用例，用例用椭圆形表达
* 使用不同的线条表达不同的关系。包括参与者与用例的关系，用例与用例的关系

## 流程图示例

```plantuml
title 流程图

(*) --> "步骤1处理"
--> "步骤2处理"
if "条件1判断" then
    ->[true] "条件1成立时执行的动作"
    if "分支条件2判断" then
        ->[no] "条件2不成立时执行的动作"
        -> === 中间流程汇总点1 ===
    else
        -->[yes] === 中间流程汇总点1 ===
    endif
    if "分支条件3判断" then
        -->[yes] "分支条件3成立时执行的动作"
        --> "Page.onRender ()" as render
        --> === REDIRECT_CHECK ===
    else
        -->[no] "分支条件3不成立时的动作"
        --> render
    endif
else
    -->[false] === REDIRECT_CHECK ===
endif

if "条件4判断" then
    ->[yes] "条件4成立时执行的动作"
    --> "流程最后结点"
else
endif
--> "流程最后结点"
-->(*)
```

## 流程图新语法示例

```plantuml
title 流程图

start
:"步骤1处理";
:"步骤2处理";
if("条件1判断") then (true)
    :"条件1成立时执行的动作";
    if (分支条件2判断) then (false)
        :"条件2不成立时执行的动作";
    else
    endif
    :=== 中间流程汇总点1 ===;
    if (分支条件3判断) then (true)
        :"分支条件3成立时执行的动作";
    else (false)
        :"分支条件3不成立时的动作";
    endif
    :"Page.onRender ()";
else (false)
endif

if (条件4判断) then (true)
    :"条件4成立时执行的动作";
else
endif
:"流程最后结点";
stop
```

```plantuml
title 流程图

start
:"步骤1处理";
:"步骤2处理";
if ("条件1判断") then (true)
    :条件1成立时执行的动作;
    if ("分支条件2判断") then (no)
        :"条件2不成立时执行的动作";
    else (yes)
        if ("条件3判断") then (yes)
            :"条件3成立时的动作";
        else (no)
            :"条件3不成立时的动作";
        endif
    endif
    :"顺序步骤3处理";
endif

if ("条件4判断") then (yes)
:"条件4成立的动作";
else
    if ("条件5判断") then (yes)
        :"条件5成立时的动作";
    else (no)
        :"条件5不成立时的动作";
    endif
endif
stop
```

TIPS：

* 使用 start 来表示流程开始，使用 stop 来表示流程结束
* 顺序流程使用冒号和分号 :xxx; 来表示
* 条件语句使用 if ("condition 1") then (true/yes/false/no) 来表示
* 条件语句可以嵌套

## 组件图示例

```plantuml
title 组件图

package "组件1" {
    ["组件1.1"] - ["组件1.2"]
    ["组件1.2"] -> ["组件2.1"]
}

node "组件2" {
    ["组件2.1"] - ["组件2.2"]
    ["组件2.2"] --> [负载均衡服务器]
}

cloud {
    [负载均衡服务器] -> [逻辑服务器1]
    [负载均衡服务器] -> [逻辑服务器2]
    [负载均衡服务器] -> [逻辑服务器3]
}

database "MySql" {
    folder "This is my folder" {
        [Folder 3]
    }

    frame "Foo" {
        [Frame 4]
    }
}

[逻辑服务器1] --> [Folder 3]
[逻辑服务器2] --> [Frame 4]
[逻辑服务器3] --> [Frame 4]
```

TIPS：

* 使用方括号 [xxx] 来表示组件
* 可以把几个组件合并成一个包，可以使用的关键字为 package, node, folder, frame, cloud, database。不同的关键字图形不一样。
* 可以在包内部用不同的箭头表达同一个包的组件之间的关系
* 可以在包内部直接表达到另外一个包内部的组件的交互关系
* 可以在流程图外部直接表达包之间或包的组件之间的交互关系

## 状态图示例

我们一般使用状态图来画状态机

```plantuml
title 状态图


[*] --> NotShooting

state NotShooting {
    [*] --> Idle
    Idle --> Processing: SignalEvent
    Processing --> Idle: Finish
    Idle --> Configuring : EvConfig
    Configuring --> Idle : EvConfig
}

state Configuring {
    [*] --> NewValueSelection
    NewValueSelection --> NewValuePreview : EvNewValue
    NewValuePreview --> NewValueSelection : EvNewValueRejected
    NewValuePreview --> NewValueSelection : EvNewValueSaved
    state NewValuePreview {
        State1 -> State2
    }
}
```

TIPS：

* 使用 [*] 来表示状态的起点
* 使用 state 来定义子状态图
* 状态图可以嵌套
* 使用 scale 命令来指定生成的图片的尺寸

不需要去记这些标记，在需要的时候去使用它，通过不断地使用来熟悉不同的图的语法。可以下载 PlanUML 官方文档 作为参考，遇到问题的时候翻一翻，这样很快就可以学会使用 PlantUML 高效地画图。
