# Cubic Bézier Curve

## Proof of formula

### Formula
This is the formula of a cubic bézier curve we are aiming to proof:
$$P(t) = (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3$$

### Linear interpolation

Linear interpolation (lerp) is defined as a linear parametrization of the line between two points.
Therefore, it can be described by two points $P_0, P_1$ and a parameter $t$.
The t-value can be thought of as a percentage of how much the point $P$ it is on the way to $P_1$.

$$ P(t) = (1-t)P_0 + tP_1$$

### De Casteljau's algorithm
[De Casteljau's algorithm](https://en.wikipedia.org/wiki/De_Casteljau%27s_algorithm) provides an elegant approach for constructing bezier curves.
It does it recursively, as follows:

For every $t \in [0,1]$
1. First, start with $n$ points $P_0, P_1, ..., P_{n-1}$
2. Lerp between each line segment $\overline{P_0P_1}, \overline{P_1P_2}, ..., \overline{P_{n-2}P_{n-1}}$ using parameter $t$.
3. Go to step 1 with $n-1$ new points

The recursion ends when there is exactly one point left — $P(t)$.

### Proof
Using De Casteljau's algorithm, we can deduce the formula of a cubic bezier curve. We start with four points $P_0, P_1, P_2, P_3$.

Iteration #1

$$\eqalign{
A=(1-t)P_0+tP_1 \\
B=(1-t)P_1+tP_2 \\
C=(1-t)P_2+tP_3
}$$


Iteration #2

$$\eqalign{
D &= (1-t)A+tB \\
        &= (1-t)^2P_0+(1-t)tP_1 + t(1-t)P_1+t^2P_2 \\
        &= (1-t)^2P_0+2(1-t)tP_1+t^2P_2
}$$

$$\eqalign{
E &= (1-t)B+tC \\
        &= (1-t)^2P_1+(1-t)tP_2 + t(1-t)P_2+t^2P_3 \\
        &= (1-t)^2P_1+2(1-t)tP_2+t^2P_3
}$$


Iteration #3

$$\eqalign{
P &= (1-t)D+tE \\
        &= (1-t)^3P_0+2(1-t)^2tP_1+(1-t)t^2P_2 \\
& \; + (1-t)^2tP_1+2(1-t)t^2P_2+t^3P_3 \\
        &= (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3
}$$

Thus, we arrive at the [Bernstein polynomial form](https://en.wikipedia.org/wiki/Bernstein_polynomial) of a cubic bezier curve:

$$P(t) = (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3$$


 
## Proof of C<sup>1</sup> continuity
[Cubic Bézier Curve C<sup>1</sup> Continuity Proof](https://docs.google.com/document/d/1yOPxu6LAcAWaRyBlGrb4e02S1lrvkTArEI2bsm8eq4w/edit?usp=sharing)
