# Cubic Bézier Curve

## Proof of formula

### Formula
This is the formula of the cubic bézier curve we are aiming to proof:
$$P(t) = (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3$$

### Linear interpolation

Linear interpolation (lerp) is defined as a linear parametrization of the line between two points.
Therefore, it can be described by two points $P_0, P_1$ and a parameter $t$.
The t-value can be thought of as a percentage of how much the point $P$ it is on the way to $P_1$.

$$ P(t) = (1-t)P_0 + tP_1$$

### Proof

First lerp

$$A=(1-t)P_0+tP_1$$

$$B=(1-t)P_1+tP_2$$

$$C=(1-t)P_2+tP_3$$


Second lerp

$$D=(1-t)A+tB$$

$$E=(1-t)B+tC$$



Third lerp

$$F=(1-t)D+tE$$


## Proof of C1 continuity
[Cubic Bézier Curve C1 Continuity Proof](https://docs.google.com/document/d/1yOPxu6LAcAWaRyBlGrb4e02S1lrvkTArEI2bsm8eq4w/edit?usp=sharing)
