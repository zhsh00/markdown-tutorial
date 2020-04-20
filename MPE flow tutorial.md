---
toc:
  depth_from: 2
  depth_to: 4
  ordered: false
---

# MPE

[TOC]

## flow流程图示例

### 定义元素的语法

格式： 变量=>操作块: 备注名
或
tag=>type: content:>url

tag就是元素名字，
type是这个元素的类型，有6中类型，分别为：
start # 开始
end # 结束
operation # 操作
subroutine # 子程序
condition # 条件
inputoutput # 输入或输出[平行四边形]
content就是在框框中要写的内容，注意type后的冒号与文本之间一定要有个空格。
url是一个连接，与框框中的文本相绑定

st=>start: 开始
e=>end: 结束
普通操作块 opration
op1=>opration: 第一个操作块
op2=>opration: 第二个操作块
判断块 condition
cond1=>condition: 第一个判断
cond2=>condition: 第二个判断
输入输出块 inputoutput[平行四边形]
io1=>inputoutput: 输入输出块1
io2=>inputoutput: 输入输出块2
子任务块
sub1=>subroutine: 子任务1
sub2=>subroutine: 子任务2

### 连接元素的语法

用->来连接两个元素，需要注意的是condition类型，因为他有yes和no两个分支，所以要写成
c2(yes)->io->e
c2(no)->op2->e
分着写
c2(yes)->io
io->e
c2(no)->op2
op2->e

### 位置控制

cond1(no)->op2(right)->op1 #控制 op2 位置置于右边，再由op2 返回 op1 (好像不能向左)
还可以这样 cond1(no,right)
cond1(yes)->e

### 示例

```flow
st=>start: 开始
e=>end: over
st->e
```

```flow
st=>start: 开始
e=>end: over
io=>inputoutput: 输入年份
st->io->e
```

```flow
st=>start: 开始
e=>end: over
io=>inputoutput: 输入年份
cond4=>condition: n能否被4整除?
cond100=>condition: n能否被100整除?
cond400=>condition: n能否被400整除?
leap=>inputoutput: 输出闰年
notleap=>inputoutput: 输出非闰年
notleap2=>inputoutput: 输出非闰年
st->io->cond4(yes)->cond100(yes)->cond400(no, left)->notleap
st->io->cond4(no)->notleap2
cond100(no)->leap
cond400(yes)->leap
leap->e
notleap->e
notleap2->e
```

```flow
st=>start: 鉴权
e=>end: 结束退出
cond1=>condition: user==bgbiao
product=ddaotian
productcheck=>condition: ddaotian类型产品库存
(ecs,bss,vpc,eip,hids)
  
  
op1=>operation: 发起预订请求
拆单并库存检测
  
op2=>operation: info:生产指定类型产品
(DAOTIAN:ecs,natip,eip,hids)
op3=>operation: 鉴权失败
op4=>operation: 库存检测失败
  
io1=>inputoutput: 返回产品相关信息
ECS,NATIP,EIP,HIDS
  
io2=>inputoutput: info:无此类型产品
  
  
  
st->cond1
cond1(yes)->op1->productcheck(yes)->op2->io1->e
cond1(no)->op3->e
cond1(yes)->op1->productcheck(no)->op4->io2->e
```

```flow
st=>start: Start|past:>http://www.google.com[blank]
e=>end: End:>http://www.google.com
op1=>operation: get_hotel_ids|past
op2=>operation: get_proxy|current
sub1=>subroutine: get_proxy|current
op3=>operation: save_comment|current
op4=>operation: set_sentiment|current
op5=>operation: set_record|current

cond1=>condition: ids_remain空?
cond2=>condition: proxy_list空?
cond3=>condition: ids_got空?
cond4=>condition: 爬取成功??
cond5=>condition: ids_remain空?

io1=>inputoutput: ids-remain
io2=>inputoutput: proxy_list
io3=>inputoutput: ids-got

st->op1(right)->io1->cond1
cond1(yes)->sub1->io2->cond2
cond2(no)->op3
cond2(yes)->sub1
cond1(no)->op3->cond4
cond4(yes)->io3->cond3
cond4(no)->io1
cond3(no)->op4
cond3(yes, right)->cond5
cond5(yes)->op5
cond5(no)->cond3
op5->e
```
