# 使用UV刪除相機外的點

# 使用UV刪除相機外的點

刪體積用volume節點配合volume mix/vdb combine去刪除會比較方便
---

![](https://i.imgur.com/MTlr7Ul.png)

point wrangle:
---

```
float margin = chf('margin');
if (@uv.z == 0) removepoint(0,@ptnum);
if (@uv.x < -margin || @uv.x > 1+margin) removepoint(0,@ptnum);
if (@uv.y < -margin || @uv.y > 1+margin) removepoint(0,@ptnum);
```

###### tags: `Houdini` `vex`
