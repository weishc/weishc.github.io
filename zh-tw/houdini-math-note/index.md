# Houdini 數學應用筆記

# Houdini 數學應用筆記


dot product 判斷v大致方向（銳角or鈍角）
---

假設要判斷@v與x軸為銳角or鈍角

x=(1,0,0)

if (@v dot x) >0 =往x軸 else ＝ 往反向

dot product 求兩向量之夾角
---
```
vector a = set(0,1,0);
vector b = set(1,0,0);
f@angle=degrees(acos(dot(a, b)/length(a)*length(b)));
```

@angle=90

也可寫成

```
vector a = normalize(set(0,1,0));
vector b = normalize(set(1,0,0));
f@angle=degrees(acos(dot(a, b)/a*b));
```

同理可應用在cosθ=0,1,-1分別代表同向,垂直,反向


