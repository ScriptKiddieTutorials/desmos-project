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
        &= (1-t)^3P_0+2(1-t)^2tP_1+(1-t)t^2P_2 + (1-t)^2tP_1+2(1-t)t^2P_2+t^3P_3 \\
        &= (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3
}$$

Thus, we arrive at the [Bernstein polynomial form](https://en.wikipedia.org/wiki/Bernstein_polynomial) of a cubic bezier curve:

$$P(t) = (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3$$


 
## Proof of condition for C<sup>1</sup> continuity
## Derivation of velocity vector
We aim to proof that in order for two cubic bézier curves $P_0P_1P_2P_3$ and $P_3P_4P_5P_6$ to be $C^1$ continuous (i.e. differentiable) at point $P_3$, they must satisfy

$$P_4=\frac{P_3+P_5}{2}$$


The formula we derived for a cubic bézier curve is:

$$P(t) = (1-t)^3P_0+3(1-t)^2tP_1+3(1-t)t^2P_2+t^3P_3$$


Now, instead of grouping the terms based on points, we can expand it,

$$\eqalign{
P(t) &= P_0(-t^3+3t^2-3t+1) \\
        &+P_1(3t^3-6t^2+3t)  \\
        &+P_2(-3t^3+3t^2) \\
        &+P_3(t^3)
}$$

and write it as a polynomial of $t$.

$$\eqalign{
P(t) &= (-P_0+3P_1-3P_2+P_3)t^3 \\
        &+3(P_0-2P_1+P_2)t^2  \\
        &+3(-P_0+P_1)t \\
        &+P_0
}$$

Then, take the derivative with respect to $t$. This gives the velocity vector associated at every t-value.

$$\eqalign{
P'(t) &= 3(-P_0+3P_1-3P_2+P_3)t^2 \\
        &+6(P_0-P_1+P_2)t  \\
        &+3(-P_0+P_1)
}$$

## Proof
Let’s label the points of the first bézier curve $P_0, P_1, P_2, P_3$, and that of the second $P_3, P_4, P_5, P_6$. In order for them to be $C^1$ continuous, their velocities must be equal at $P_3$, where the end ($t=1$) of the first curve meets the start ($t=0$) of the second curve. We can write it as an equation:

$$P_1(1)=P_2(0)$$

We can plug in the formula for the velocity vector and evaluate them at t=1 and t=0 respectively.

$$\eqalign{
&3(-P_0+3P_1-3P_2+P_3)(1)^2+6(P_0-P_1+P_2)(1)+3(-P_0+P_1) \\
= &3(-P_3+3P_4-3P_5+P_6)(0)^2+6(P_3-P_4+P_5)(0)+3(-P_3+P_4)
}$$

Then, collect like terms on either side

$$-3P_2+3P_3 = -3P_3+3P_4$$

Finally, simplify

$$P_4 = \frac{P_3+P_5}{2}$$

We have derived a necessary and sufficient condition for two cubic bézier curves to be $C^1$ continuous.
