
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
(1..10).flatMap { i -> (4..20).map { j -> 2 *i * j } }.sum()
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

### Decorators

Sometimes a variable can have "decorators" to further add meaning to a variable but with standardized conciseness.

#### "Hat" Symbol

The hat symbol, such as <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\hat&space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\hat&space;x" title="\hat x" /></a>, is often used to indicate a predicted value as opposed to an actual. This is often in the context of prediction and forecasting a number. You could simply express a predicted and actual value as <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x_{predicted}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x_{predicted}" title="x_{predicted}" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x_{actual}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x_{actual}" title="x_{actual}" /></a>, but it can be much more concise to use a `^` symbol. 

For example, say we predict selling <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\hat&space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\hat&space;x" title="\hat x" /></a> products, but in actuality we sell <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;x" title="x" /></a>. Our forecast error would be the difference between these two variables. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\text{Forecast&space;Error}&space;=&space;\hat&space;x&space;-&space;x" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\text{Forecast&space;Error}&space;=&space;\hat&space;x&space;-&space;x" title="\text{Forecast Error} = \hat x - x" /></a>

### Greek Letters

The Greek alphabet can be used as variables (and sometimes operators) as well. There is little consistency on how they are used and for what. However, there are some common usages for certains symbols as documented in this table. 

| Uppercase | Lowercase | Name    | Common Usage |
|-----------|-----------|---------|--------------|
| Α         | α         | Alpha   |              |
| Β         | β         | Beta    |              |
| Γ         | γ         | Gamma   |              |
| Δ         | δ         | Delta   |Measurement of change or difference, derivative... [Read More](https://en.wikipedia.org/wiki/Delta_(letter)#Upper_case)|
| Ε         | ε         | Epsilon |              |
| Ζ         | ζ         | Zeta    |              |
| Η         | η         | Eta     |              |
| Θ         | θ         | Theta   |Geometric angles, trigonometric variables... [Read More](https://en.wikipedia.org/wiki/Theta#Mathematics_and_science)|
| Ι         | ι         | Iota    |              |
| Κ         | κ         | Kappa   |              |
| Λ         | λ         | Lambda  |              |
| Μ         | μ         | Mu      |              |
| Ν         | ν         | Nu      |              |
| Ξ         | ξ         | Xi      |              |
| Ο         | ο         | Omicron |              |
| Π         | π         | Pi      |              |
| Ρ         | ρ         | Rho     |              |
| Σ         | σ/ς       | Sigma   |Summation, standard deviation... [Read More](https://en.wikipedia.org/wiki/Sigma#Science_and_mathematics)|
| Τ         | τ         | Tau     |              |
| Υ         | υ         | Upsilon |              |
| Φ         | φ         | Phi     |              |
| Χ         | χ         | Chi     |              |
| Ψ         | ψ         | Psi     |              |
| Ω         | ω         | Omega   |              |


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

Linear algebra takes the tediousness out of working with large multidimensional arrays of numbers and manipulating them with transformations. While you can certainly iterate these numbers yourself and perform whatever calculation you need, it can become extremely inefficient and cumbersome to do yourself. 

There are great libraries that can do this for you. In the Python world you would typically use [NumPy](http://www.numpy.org/). In the JVM world, you can use [ND4J](http://nd4j.org/), [ojAlgo](https://github.com/optimatika/ojAlgo), or [JBlas](http://jblas.org/). The Kotlin multiplatform library [Koma](https://github.com/kyonifer/koma) will probably be your go-to if you intend on doing linear algebra in Kotlin. 

If you want to learn more about Linear Algebra, [3Blue1Brown](https://www.youtube.com/watch?v=fNk_zzaMoSs&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) has a great video series on linear algebra on YouTube. 

### Scalars

A scalar is simply a single number (as opposed to an array of numbers which is called a vector). Declaring a scalar value in Kotlin is no different than declaring a numeric variable, such as an `Int` or `Double`.

In linear algebra, scalars are often used in the context of multiplication (hence the name _scalar_, because they _scale_ things). 

```kotlin 
// all these assignments are scalars
val increaseRate = 1.04

val oldSpeed = 60.0

val newSpeed = oldSpeed * increaseRate
```


### Vectors

In strict programming terms, a vector is an array of numeric values often representing values of different variables. 

```kotlin
// kotlin-stdlib
val myVector = doubleArrayOf(1.0, 5.2, 2.4)

//koma 
val myVector = rowVectorOf(1.0, 5.2, 2.4)
```

By _variables_, we may be talking about _observations_. For instance, we can have a vector of temperatures for a given week.  

```kotlin
// kotlin-stdlib
val lowTemperatures = intArrayOf(67, 62, 71, 73, 64, 66, 64)
val highTemperatures = intArrayOf(76, 74, 77, 75, 76, 73, 72)

// koma
val lowTemperatures = rowVectorOf(67, 62, 71, 73, 64, 66, 64)
val highTemperatures = rowVectorOf(76, 74, 77, 75, 76, 73, 72)
```

We can also represent different attribributes of an item with a vector. For example, we can express a color in terms of three RGB values. 

```kotlin

// kotlin-stdlib
val pinkColor = intArrayOf(255, 175, 175)

// koma
val pinkColor = rowVectorOf(255, 175, 175)
```

We can also express different attributes of a `Person`: 

```kotlin
// height and weight of a person

// kotlin-stdlib
val personalAttributes = doubleArrayOf(71.5, 181.3)

// koma
val personalAttributes = rowVectorOf(71.5, 181.3)
```

So why do we express things in terms of vectors rather than classes with properties? When it comes to heavy number-crunching (e.g. machine learning), raw numbers are far more efficient and standardized to compute with. Typically, vectors and matrices (covered next) are binded to a C library that can iteratively do math efficiently. 

#### Vector Math

Adding/multipliying a vector with a scalar simply results in a vector with each value added/multiplied respectively by that scalar. 

```kotlin
val populations = rowVectorOf(2310, 2387, 5732)
val growthRate = 1.01

val newPopulations = populations * growthRate

println(newPopulations) // mat[ 2333.10,  2410.87,  5789.32 ]
```

If the dimenstions match, you can sum each respective element together (kind of like zipping) between two vectors using a `+` operator: 

```kotlin
val adultPopulations = rowVectorOf(2323, 5672, 2345)
val childPopulations = rowVectorOf(1632, 1252, 1658)

val totalPopulations = adultPopulations + childPopulations

println(totalPopulations) // mat[ 3955.00,  6924.00,  4003.00 ]
```

However using a multiplication operator `*` with two vectors will not work like you probably expect. It does not zip and multiply respective elements together, but rather performs a dot product (which we will cover later). If we multiply two vectors of the same length, it throws an error:

```kotlin 
val populations = rowVectorOf(2310, 2387, 5732)
val growthRates = rowVectorOf(1.03, 1.06, 1.09)

val newPopulations = populations * growthRates // ERROR! #columns != #rows

println(newPopulations)
```

If you want to zip and multipy each element respectively, use the `elementTimes()` operator. 

```kotlin 
val populations = rowVectorOf(2310, 2387, 5732)
val growthRates = rowVectorOf(1.03, 1.06, 1.09)

val newPopulations = populations.elementTimes(growthRates)

println(newPopulations)
```

### Matrices

TODO

### Dot Products 


# Calculus

Calculus is the study of _change_ in mathematics, studying rates of change and how a change in one variable affects another variable.

Rates of change and deriving functions that calculate rate of change is the core of calculus. It is useful in machine learning and optimization, so unsurprisingly calculus has been getting a lot of interest outside of academia. When you are trying to minimize error in your machine learning algorithm, you have to increase or decrease parameters to minimize the error. Rather than hopelessly trying every possible combination of parameters to find the lowest resulting error, it can be much more efficient to leverage rate of change in error. With that rate, you can determine if a given point is increasing/decreasing in error and use that as your compass. Then you know which direction to tune your parameters. 

 [3Blue1Brown has a fun YouTube series on Calculus fundamentals](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr).


### Derivatives

Programming with math often models things as functions, such as <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;f(x)&space;=&space;3x&space;&plus;&space;10" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;f(x)&space;=&space;3x&space;&plus;&space;10" title="f(x) = 3x + 10" /></a>. You can be trying to fit data to a linear function <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;y&space;=&space;mx&space;&plus;&space;b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;y&space;=&space;mx&space;&plus;&space;b" title="y = mx + b" /></a>, or minimizing a function measuring error in a neural network. 

However, when dealing with nonlinear functions (which represent a curvy line or plane, not a straight or flat one), we are often interested in finding the lowest or highest point for optimization reasons. Knowing the slope at a given point on that line or plane can help you follow the steepest direction and find that minimum or maximum. 

### Partial Derivatives

### Integrals

