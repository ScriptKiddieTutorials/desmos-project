# desmos-project

## Cubic Bézier Curve

### Proof of formula
This is the formula of the cubic bézier curve we are aiming to proof:
$$P(t) = (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3$$


First lerp

```math
A=(1-t)P_0+tP_1 \\
B=(1-t)P_1+tP_2 \\
C=(1-t)P_2+tP_3
```


Second lerp

```math
D=(1-t)A+tB \\
E=(1-t)B+tC
```


Final lerp

```math
F=(1-t)D+tE
```



### Proof of C1 continuity
[Cubic Bézier Curve C1 Continuity Proof](https://docs.google.com/document/d/1yOPxu6LAcAWaRyBlGrb4e02S1lrvkTArEI2bsm8eq4w/edit?usp=sharing)
