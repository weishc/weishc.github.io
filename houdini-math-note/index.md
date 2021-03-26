# Houdini math note

# Houdini math note


dot product:Determine the general direction of velocity.(acute angle or obtuse angle)
---

In order to determine that the Angle between @v and the X-axis is acute or obtuse.

x=(1,0,0)

if (@v dot x) > 0 = +x, else ＝ opposite direction

dot product Find the angle between two vectors.
---
```
vector a = set(0,1,0);
vector b = set(1,0,0);
f@angle=degrees(acos(dot(a, b)/length(a)*length(b)));
```

@angle=90

Also, it can be written as:

```
vector a = normalize(set(0,1,0));
vector b = normalize(set(1,0,0));
f@angle=degrees(acos(dot(a, b)/a*b));
```

Similarly, when cos = 0,1, and -1, they are going in the same direction, perpendicular, and opposite.


