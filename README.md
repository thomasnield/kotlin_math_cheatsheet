# Math → Kotlin Cheatsheet


## Summation

This symbol <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\sum" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\sum" title="\sum" /></a> indicates you are summing a series of items. It is probably one of the most commonly used symbols in math to express iterative addition. 


|Math Expression|Kotlin Code|
|---|---|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{n=1}^{3}n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{n=1}^{3}n" title="\sum_{n=1}^{3}n" /></a>|`(1..3).sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{n=1}^{5}10n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{n=1}^{5}10n" title="\sum_{n=1}^{5}10n" /></a>|`(1..5).map { n -> 10*n }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=0}^{n}n^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=0}^{n}n^2" title="\sum_{i=0}^{n}n^2" /></a>|`fun f(n: Int) = (0..n).map { it * it }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{n=1}^{100}3x^2&space;&plus;&space;2n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{n=1}^{100}3x^2&space;&plus;&space;2n" title="\sum_{n=1}^{100}3x^2 + 2n" /></a>|`fun f(x: Double) = (1..100).map { n -> 3 * Math.pow(x, 2.0) + (2*n) }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=100&space;&plus;&space;3\sum_{i=0}^{n}n^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?10&space;&plus;&space;3\sum_{i=0}^{n}n^2" title="10 + 3\sum_{i=0}^{n}n^2" /></a>|        `fun f(n: Int) = 10 + 3*(0..n).map { it * it }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=0}^{n}&space;x_i&space;&plus;&space;n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=0}^{n}&space;x_i&space;&plus;&space;n" title="\sum_{i=0}^{n} x_i + n" /></a>|`fun f(allX: List<Int>) = allX.mapIndexed { n,x -> x*x + n }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{10}&space;\sum_{j=4}^{20}&space;2ij" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{4}&space;\sum_{j=4}^{20}&space;2ij" title="\sum_{i=1}^{10} \sum_{j=4}^{20} 2ij" /></a>|`(1..4).flatMap { i -> (4..20).map { j -> 2 *i * j } }.sum()`|

### Nested Summation

When you see more than one summation, this means they are nested summations. This is no different than summing with nested loops or flatmapped functional sequences. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{10}&space;\sum_{j=4}^{20}&space;2ij" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{10}&space;\sum_{j=4}^{20}&space;2ij" title="\sum_{i=1}^{10} \sum_{j=4}^{20} 2ij" /></a>

```kotlin
(1..4).flatMap { i -> (4..20).map { j -> 2 *i * j } }.sum()
```



## Variables 

Hopefully the concept of a variable (such as `x`) should be self-explanatory to a programmer. However, in mathematical notation it is common for subscripts to distinctly describe several instances of that variable. 

An example, we can define 5 different variables all named <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x" title="x" /></a>, but notate them as <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x_1,&space;x_2,&space;x_3,&space;x_4,&space;\text{and}&space;x_5" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x_1,&space;x_2,&space;x_3,&space;x_4,&space;\text{and}&space;x_5" title="x_1, x_2, x_3, x_4, \text{and} x_5" /></a>. Here is how we can notate an average operation.

**Calculating an Average of 5 Variables**

<a href="https://www.codecogs.com/eqnedit.php?latex=x_{average}&space;=&space;\frac{x_1&space;&plus;&space;x_2&space;&plus;&space;x_3&space;&plus;&space;x_4&space;&plus;&space;x_5}{5}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{average}&space;=&space;\frac{x_1&space;&plus;&space;x_2&space;&plus;&space;x_3&space;&plus;&space;x_4&space;&plus;&space;x_5}{5}" title="x_{average} = \frac{x_1 + x_2 + x_3 + x_4 + x_5}{5}" /></a>. 

```kotlin
val xValues = listOf(23, 65, 45, 23, 66)
val xAverage = allXs.sum() / 5 
```


## Elements and Sets 

## Functions



|Math Expression|Description|Kotlin Code|
|---|---|---|
|<a href="https://www.codecogs.com/eqnedit.php?latex=e^x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?e^x" title="e^x" /></a>|Exponent of `e`|`exp(x)`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=ln(x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?ln(x)" title="ln(x)" /></a>|Natural logarithm|`ln(x)`|


## Symbols 

## Linear Algebra

