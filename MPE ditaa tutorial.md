---
toc:
  depth_from: 2
  depth_to: 4
  ordered: false
---

# ditaa

[TOC]

## ditaa示例

```ditaa {cmd=true run_on_save=true args=["-E"]}
  +--------+   +-------+    +-------+
  |        | --+ ditaa +--> |       |
  |  Text  |   +-------+    |diagram|
  |Document|   |!magic!|    |       |
  |     {d}|   |       |    |       |
  +---+----+   +-------+    +-------+
      :                         ^
      |       Lots of work      |
      +-------------------------+
```

```ditaa {cmd=true run_on_save=true args=["-E"]}
Color codes
/-------------+-------------\
|cRED RED     |cBLU BLU     |
+-------------+-------------+
|cGRE GRE     |cPNK PNK     |
+-------------+-------------+
|cBLK BLK     |cYEL YEL     |
\-------------+-------------/
```

```ditaa {cmd=true run_on_save=true args=["-E"]}
/-----------------\
| Things to do    |
| cGRE            |
| o Cut the grass |
| o Buy jam       |
| o Fix car       |
| o Make website  |
\-----------------/
```

```ditaa {cmd=true run_on_save=true args=["-E"]}
*----*
|    |      /--*
*    *      |
|    |  -*--+
*----*
```
