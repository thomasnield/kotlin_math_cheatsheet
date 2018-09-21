# Math -> Kotlin Cheatsheet


## Summation

This symbol <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\sum" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\sum" title="\sum" /></a> indicates you are summing a series of items. 


|Math Expression|Kotlin Code|
|---|---|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{n=1}^{3}n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{n=1}^{3}n" title="\sum_{n=1}^{3}n" /></a>|`(1..3).sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{n=1}^{5}10n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{n=1}^{5}10n" title="\sum_{n=1}^{5}10n" /></a>|`(1..5).map { n -> 10*n }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{i=0}^{n}n^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{i=0}^{n}n^2" title="\sum_{i=0}^{n}n^2" /></a>|`fun f(n: Int) = (0..n).map { it * it }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=\sum_{n=1}^{100}3x^2&space;&plus;&space;2n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sum_{n=1}^{100}3x^2&space;&plus;&space;2n" title="\sum_{n=1}^{100}3x^2 + 2n" /></a>|`fun f(x: Double) = (1..100).map { n -> 3 * Math.pow(x, 2.0) + (2*n) }.sum()`|
|<a href="https://www.codecogs.com/eqnedit.php?latex=100&space;&plus;&space;3\sum_{i=0}^{n}n^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?10&space;&plus;&space;3\sum_{i=0}^{n}n^2" title="10 + 3\sum_{i=0}^{n}n^2" /></a>|        `fun f(n: Int) = 10 + 3*(0..n).map { it * it }.sum()`|
