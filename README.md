
![](http://i.imgur.com/v3FqiEA.png)

# Math → Kotlin Cheatsheet

This is still very much a work-in-progress and I welcome any contributions. This cheat sheet was inspired by [Jam3's Math as Code project](https://github.com/Jam3/math-as-code). 

I am using this [online LaTeX equation editor](https://www.codecogs.com/eqnedit.php) to generate expressions, and if you want to learn MathJax notation [here is a great resource](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference).

While you are here, please rally this [issue on Dokka](https://github.com/Kotlin/dokka/issues/245) to bring MathJax support to Kotlin Docs. 

> Please note that these code examples may leave out some optimizations (e.g. using [collection operators instead of Sequences](https://winterbe.com/posts/2018/07/23/kotlin-sequence-tutorial/#sequences-vs-collections)) in order to reduce boilerplate and make concepts clear. 

# Understanding Math Expressions

Think of mathematical notation as a form of pseudocode. It is often expressing an algorithm in declarative form. It is important to note however that these mathematical symbols existed well before computers, and therefore may not be expressed in a programming-friendly way (e.g. using 1-based indexing versus 0-based indexing). Like pseudocode, the author can take liberties in defining what symbols mean, and any symbol can mean different things depending on the context. 

As a programmer, learning to interpret mathematical notation will help you navigate academic papers and blogs that apply mathematical concepts. This is especially the case when you dabble in machine learning, mathematical optimization, and data science. 

# Summation and Multiplication

This symbol <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\sum" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\sum" title="\sum" /></a> indicates you are summing a series of items. It is probably one of the most commonly used symbols in math to express iterative addition. 

Similarly, a <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\prod" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\prod" title="\prod" /></a> is used to multiply a series of items. 


|Math Expression|Kotlin Code|
|---|---|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{3}i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{3}i" title="\sum_{i=1}^{3}i" /></a>|`(1..3).sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{5}10i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{5}10i" title="\sum_{i=1}^{5}10i" /></a>|`(1..5).map { i -> 10*i }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=0}^{n}i^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=0}^{n}i^2" title="\sum_{i=0}^{n}i^2" /></a>|`fun f(n: Int) = (0..n).map { it.pow(2) }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{100}3x^2&space;&plus;&space;2i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{100}3x^2&space;&plus;&space;2i" title="\sum_{i=1}^{100}3x^2 + 2i" /></a>|`fun f(x: Double) = (1..100).map { i -> 3 * x.pow(2) + (2*i) }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=10&space;&plus;&space;3\sum_{i=0}^{n}i^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?10&space;&plus;&space;3\sum_{i=0}^{n}i^2" title="10 + 3\sum_{i=0}^{n}i^2" /></a>|        `fun f(n: Int) = 10 + 3*(0..n).map { it * it }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=0}^{n}&space;x_i&space;&plus;&space;i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=0}^{n}&space;x_i&space;&plus;&space;i" title="\sum_{i=0}^{n} x_i + i" /></a>|`fun f(allX: List<Int>) = allX.mapIndexed { i,x -> x + i }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{10}&space;\sum_{j=4}^{20}&space;2ij" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{4}&space;\sum_{j=4}^{20}&space;2ij" title="\sum_{i=1}^{10} \sum_{j=4}^{20} 2ij" /></a>|`(1..4).flatMap { i -> (4..20).map { j -> 2 *i * j } }.sum()`<br><br>`sequence { for(i in 1..4) for (j in 4..20) yield(2 * i * j) }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\prod_{i=1}^{n}&space;i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\prod_{i=1}^{n}&space;i" title="\\prod_{i=1}^{n} i" /></a>|`(1..n).fold(1L, Long::times)`|

### Nested Summation

When you see more than one summation, this means they are nested summations. This is no different than summing with nested loops or flatmapped functional sequences. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{10}&space;\sum_{j=4}^{20}&space;2ij" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{10}&space;\sum_{j=4}^{20}&space;2ij" title="\sum_{i=1}^{10} \sum_{j=4}^{20} 2ij" /></a>

```kotlin
(1..4).flatMap { i -> (4..20).map { j -> 2 *i * j } }.sum()
```


### Indexes and Iteration

When approached with a mathematical expression, you need to consider it may not use 0-based indexing especially in the context of iterating elements. 

For instance, here is an operation that is iterating `n` elements and summing. The iteration starts at index 1.

<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{n}&space;x_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{n}&space;x_i" title="\sum_{i=1}^{n} x_i" /></a>

When translating this to code, you should interpret this as iterating all the elements starting at index 0. It does not skip the first element or start at index 1. 

```kotlin 
fun f(elements: List<Int>) = elements.sum()
```

However, when you are not working with elements but rather an actual number sequence, you should interpret this literally. When we are iterating numbers 1 through 3, we really are iterating numbers 1 through 3. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=1}^{3}i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=1}^{3}i" title="\sum_{i=1}^{3}i" /></a>

```kotlin
val sum = (1..3).sum()
```
In summary, beware of 0-index and 1-index conventions, and discern what the mathematical expression is trying to achieve before translating it into code. 


# Variables 

Hopefully the concept of a variable (such as `x`) should be self-explanatory to a programmer. However, in mathematical notation it is common for subscripts and other "decorators" to distinctly describe several instances of that variable. For instance, we can use `old` and `new` `x` values to measure a rate of change.

<a href="https://www.codecogs.com/eqnedit.php?latex=change&space;=&space;\frac{x_{new}&space;-&space;x_{old}}{x_{old}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?change&space;=&space;\frac{x_{new}&space;-&space;x_{old}}{x_{old}}" title="change = \frac{x_{new} - x_{old}}{x_{old}}" /></a>

Here is a more iterative example. We can define 5 different variables all named <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x" title="x" /></a>, but notate them as <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x_1,&space;x_2,&space;x_3,&space;x_4,&space;\text{and}&space;x_5" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x_1,&space;x_2,&space;x_3,&space;x_4,&space;\text{and}&space;x_5" title="x_1, x_2, x_3, x_4, \text{and} x_5" /></a>. Here is how we can notate an average operation.

<a href="https://www.codecogs.com/eqnedit.php?latex=x_{average}&space;=&space;\frac{x_1&space;&plus;&space;x_2&space;&plus;&space;x_3&space;&plus;&space;x_4&space;&plus;&space;x_5}{5}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{average}&space;=&space;\frac{x_1&space;&plus;&space;x_2&space;&plus;&space;x_3&space;&plus;&space;x_4&space;&plus;&space;x_5}{5}" title="x_{average} = \frac{x_1 + x_2 + x_3 + x_4 + x_5}{5}" /></a>. 

```kotlin
val xValues = listOf(23, 65, 45, 23, 66)
val xAverage = allXs.sum() / 5 

// or 

val xAverage = allXs.average()
```

Mathematics and programming are similar in that they try to generalize. Instead of formulating an average for just `5` variables, we can notate it for any `n` number of variables. 


<a href="https://www.codecogs.com/eqnedit.php?latex=x_{average}&space;=&space;\frac{x_1&space;&plus;&space;x_2&space;&plus;&space;...&space;&plus;&space;x_n}{n}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{average}&space;=&space;\frac{x_1&space;&plus;&space;x_2&space;&plus;&space;...&space;&plus;&space;x_n}{n}" title="x_{average} = \frac{x_1 + x_2 + ... + x_n}{n}"/></a>


To maximize fanciness, we can go a step further and use a summation operator and just generalize each `x` value as <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x_i" title="x_i" /></a>. Note that `n` is the number of variables/elements we are averaging. 


<a href="https://www.codecogs.com/eqnedit.php?latex=x_{average}&space;=&space;\frac{1}{n}\sum_{i=1}^{n}x_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{average}&space;=&space;\frac{1}{n}\sum_{i=1}^{n}x_i" title="x_{average} = \frac{1}{n}\sum_{i=1}^{n}x_i" /></a>


### Special Variable Symbols 

#### Greek Letters

The Greek alphabet can be used as variable names as well, and there is little consistency on how they are used and for what. For instance, 


#### Theta 

<a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\theta" title="\theta" /></a> (called "Theta") is sometimes for constants, special variables, or [polar angles](https://en.wikipedia.org/wiki/Spherical_coordinate_system). 

A place you will definitely see theta used is in trigonometric equations like <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;cos(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;cos(\theta)" title="cos(\theta)" /></a>, <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;sin(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;sin(\theta)" title="sin(\theta)" /></a>, and <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;tan(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;tan(\theta)" title="tan(\theta)" /></a>. 

### Naming Variables in Kotlin 

Trying to express variables like <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x_1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x_1" title="x_1" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x_{old}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x_{old}" title="x_{old}" /></a> can be a little awkward in code. In Kotlin, you can choose to stick with conventional camelCase or break style guidelines by using underscores. 

```kotlin
val x1 = 12
val x_1 = 12

val xOld = 13
val x_old = 13
```
For mathematical symbols like theta <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\theta" title="\theta" /></a>, you can just name your variable `theta`. 

```kotlin 
import kotlin.math.PI
import kotlin.math.sin 

val theta = PI / 2.0
val result = sin(theta)
```

Hopefully you will not run into this decision of naming variables often, as you may express variables as iterated elements in collections/sequences rather than give each one an explicit variable name. 


# Elements and Sets 

TODO

# Functions


|Math Expression|Description|Kotlin Code|
|---|---|---|
|<a href="https://www.codecogs.com/eqnedit.php?latex=e^x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?e^x" title="e^x" /></a>|Exponent of `e`|`exp(x)`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=ln(x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?ln(x)" title="ln(x)" /></a>|Natural logarithm|`ln(x)`|



# Linear Algebra

Linear algebra is the building block of machine learning, computer graphics, linear programming, and many other mathematically-intense computer science disciplines. Linear algebra can seem pointless until you apply it to specific problems. For example, a neural network is typically executed using dot products to multiply and sum weights and node values. 

Linear algebra takes the tediousness out of working with large multidimensional arrays of numbers. While you can certainly iterate these numbers yourself and perform whatever calculation you need, it can become extremely inefficient and tedious to do yourself. 

There are great libraries that can do this for you. In the Python world you would typically use [NumPy](http://www.numpy.org/). In the JVM world, you can use [ND4J](http://nd4j.org/), [ojAlgo](https://github.com/optimatika/ojAlgo), or [JBlas](http://jblas.org/). The Kotlin multiplatform library [Koma](https://github.com/kyonifer/koma) will probably be your go-to if you intend on doing linear algebra in Kotlin. 

> If you want to learn more, [3Blue1Brown](https://www.youtube.com/watch?v=fNk_zzaMoSs&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) has a great video series on linear algebra on YouTube. 

### Vectors

TODO

### Matrices

TODO

### Matrix Operators

TODO
