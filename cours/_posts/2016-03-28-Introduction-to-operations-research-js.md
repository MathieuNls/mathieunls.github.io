---
layout: post
title: An introduction to operations research using Javascript
tags:
- javascript
- linear regression
- simplex
- dynamic programming
- knapsack
description: An introduction to operations research using Javascript
image:
  feature: knap.jpg
  credit: Wikipedia
  creditlink: https://commons.wikimedia.org/wiki/File:%D0%9A%D0%BE%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%B8%D0%BA%D0%BE%D0%B2._%D0%98%D1%81%D1%82%D0%BE%D1%80%D0%B8%D1%8F_%D0%BE%D0%B4%D0%BD%D0%BE%D0%B3%D0%BE_%D0%B8%D0%B7%D0%BE%D0%B1%D1%80%D0%B5%D1%82%D0%B5%D0%BD%D0%B8%D1%8F_(1938)._%D1%81%D1%82%D1%80._55.jpg
excerpt: Operations research, or operational research in British usage, is a discipline that deals with the application of advanced analytical methods to help make better decisions. Further, the term 'operational analysis'
---
{% include _toc.html %}

# Preface

*Operations research, or operational research in British usage, is a discipline that deals with the application of advanced analytical methods to help make better decisions. Further, the term 'operational analysis' is used in the British (and some British Commonwealth) military, as an intrinsic part of capability development, management and assurance. In particular, operational analysis forms part of the Combined Operational Effectiveness and Investment Appraisals (COEIA), which support British defense capability acquisition decision-making. * [^1]

[^1]: <https://www.wikiwand.com/en/Operations_research>

As computer scientists or developer' operation research is often (always?) Related to optimization problems:
How to do the Y operation given X constraints with a maximum Z benefit.

As a concrete example:

{% highlight js %}
Maximize p = 0.5x + 3y + z + 4w subject to
x + y + z + w <= 40
-2x - y + z + w <= 10
y - w <= 10
{% endhighlight %}

In this practical introduction, we'll see how to use the Knapsack[^2] and the Simplex[^3] algorithms.

# Knapsack

*The knapsack problem or rucksack problem is a problem in combinatorial optimization: Given a set of items, each with a weight and a value, determine the number of each item to include in a collection so that the total weight is less than or equal to a given limit and the total value is as large as possible. It derives its name from the problem faced by someone who is constrained by a fixed-size knapsack and must fill it with the most valuable items.* [^2]

[^2]: <https://www.wikiwand.com/en/Knapsack_problem#/0.2F1_Knapsack_Problem>

## Solving

0/1 knapsack problem
A similar dynamic programming solution for the 0/1 knapsack problem also runs in pseudo-polynomial time. Assume w1,w,...,wn. W are strictly positive integers. Define m[i,w] to be the maximum value that can be attained with weight less than or equal to w using items up to i (first i items).

We can define m[i,w] recursively as follows:

{% highlight js %}
m[0,w]=0
m[i,w]=m[i-1,w] if w_i > w (the new item is more than the current weight limit)
m[i,w]=max(m[i-1,w],m[i-1,w-w_i]+v_i) if w_i <= w.
{% endhighlight %}

The solution can then be found by calculating m[n,W]. To do this efficiently we can use a table to store previous computations.

## Implementation

The Implementation of the knapsack algorithm with dynamic programming techniques is fairly simple:


{% highlight js %}
// Input:
// Values (stored in array v)
// Weights (stored in array w)
// Number of distinct items (n)
// Knapsack capacity (W)

for j from 0 to W do:
    m[0, j] := 0

 for i from 1 to n do:
     for j from 0 to W do:
         if w[i-1] > j then:
             m[i, j] := m[i-1, j]
         else:
             m[i, j] := max(m[i-1, j], m[i-1, j-w[i-1]] + v[i-1])
{% endhighlight %}

First, we initialize the matrix to 0, then, for each case, we simply apply the following :

{% highlight js %}
m[0,w]=0
m[i,w]=m[i-1,w] if w_i > w (the new item is more than the current weight limit)
m[i,w]=max(m[i-1,w],m[i-1,w-w_i]+v_i) if w_i <= w.
{% endhighlight %}.

### Exo 1

* Implement the knapsack in javascript.
* Test it with the following variables :
  * I have 680$ to invest
  * I can buy up to 100 stock A at 50$
  * I can buy up to 10 stock B at 80$
  * I can buy up to 18 stock C at 12$
  * Stock A will gain 10% next quarter.
  * Stock B will loose 80% next quarter.
  * Stock C will gain 220% next quarter.

### Exo 2

The given pseudocode doesn't yield the result, i.e, **What is the maximum amount of money I can make ?**
Implement a function that reads the computed matrix for the result.

### Exo 3

Finally, we know what is the maximum of money we can make given the preconditions. However, we still don't know which stock to buy.
Implement a function that reads the computed matrix for the amount of stock to buy.

# Simulated Annealing

Simulated annealing (SA) is a probabilistic technique for approximating the global optimum of a given function. Specifically, it is a metaheuristic to approximate global optimization in a large search space. It is often used when the search space is discrete (e.g., all tours that visit a given set of cities). For problems where finding the precise global optimum is less important than finding an acceptable local optimum in a fixed amount of time, simulated annealing may be preferable to alternatives such as brute-force search or gradient descent. [^6]

[^6]: <https://www.wikiwand.com/en/Simulated_annealing>

*At each step, the SA heuristic considers some neighbouring state s' of the current state s, and probabilistically decides between moving the system to state s' or staying in state s. These probabilities ultimately lead the system to move to states of lower energy. Typically this step is repeated until the system reaches a state that is good enough for the application, or until a given computation budget has been exhausted.* [^6]

{% highlight js %}
Let s = s0
For k = 0 through kmax (exclusive):
T ← temperature(k ∕ kmax)
Pick a random neighbour, snew ← neighbour(s)
If P(E(s), E(snew), T) ≥ random(0, 1), move to the new state:
s ← snew
Output: the final state s
{% endhighlight %}

## Exo

* n-queen problem

# Genetic algorithm

*In the field of artificial intelligence, a genetic algorithm (GA) is a search heuristic that mimics the process of natural selection. This heuristic (also sometimes called a metaheuristic) is routinely used to generate useful solutions to optimization and search problems.Genetic algorithms belong to the larger class of evolutionary algorithms (EA), which generate solutions to optimization problems using techniques inspired by natural evolution, such as inheritance, mutation, selection and crossover.*[^3]

[^3]: <https://www.wikiwand.com/en/Genetic_algorithm>

## Initialisation

*The population size depends on the nature of the problem, but typically contains several hundreds or thousands of possible solutions. Often, the initial population is generated randomly, allowing the entire range of possible solutions (the search space). Occasionally, the solutions may be "seeded" in areas where optimal solutions are likely to be found.*[^3]
 
## Selection And Reproduction

At each generation the top n% -- according to the fitness function -- of the current pool is selected to breed a new generation.

*For instance, in the knapsack problem one wants to maximize the total value of objects that can be put in a knapsack of some fixed capacity. A representation of a solution might be an array of bits, where each bit represents a different object, and the value of the bit (0 or 1) represents whether or not the object is in the knapsack. Not every such representation is valid, as the size of objects may exceed the capacity of the knapsack. The fitness of the solution is the sum of values of all objects in the knapsack if the representation is valid, or 0 otherwise.*[^3]

Parents breed the new generation using crossover and mutation. 
*In genetic algorithms, crossover is a genetic operator used to vary the programming of a chromosome or chromosomes from one generation to the next. It is analogous to reproduction and biological crossover, upon which genetic algorithms are based. Cross over is a process of taking more than one parent solutions and producing a child solution from them.* [^4]
*Mutation is a genetic operator used to maintain genetic diversity from one generation of a population of genetic algorithm chromosomes to the next. It is analogous to biological mutation. Mutation alters one or more gene values in a chromosome from its initial state.*[^5]

[^4]: <https://www.wikiwand.com/en/Crossover_(genetic_algorithm)>
[^5]: <https://www.wikiwand.com/en/Mutation_(genetic_algorithm)>

## Exo

- Solve the knapsack problem
- Solve a TSP problem
- Prisoner Problem

# Simplex algorithm

*In mathematical optimization, Dantzig's simplex algorithm (or simplex method) is a popular algorithm for linear programming. The journal Computing in Science and Engineering listed it as one of the top 10 algorithms of the twentieth century.
The name of the algorithm is derived from the concept of a simplex and was suggested by T. S. Motzkin. Simplices are not actually used in the method, but one interpretation of it is that it operates on simplicial cones, and these become proper simplices with an additional constraint. The simplicial cones in question are the corners (i.e., the neighborhoods of the vertices) of a geometric object called a polytope. The shape of this polytope is defined by the constraints applied to the objective function.* [^5]

[^5]: <https://www.wikiwand.com/en/Simplex_algorithm>

To resolve a linear problem with the simplex method, we'll use simplex tableau.
Simplex tableaus are matrices where the first row is the objective and the remaining rows the constraints.

The following example:

{% highlight js %}
Minimize z = - 2x - 3y - 4z subject to
3x + 2y + z <= 10
2x + 5y + 3z <= 15
x, y, z >= 0
{% endhighlight %}

produces this canonical tableau

{% highlight js %}
|1 2 3 4 0  0 |
|0 3 2 1 1 0 10|
|0 2 5 3 0 1 15|
{% endhighlight %}

where columns 5 and 6 represent the basic variables s and t and the corresponding basic feasible solution is

{% highlight js %}
x=y=z=0, s = 10, t = 15
{% endhighlight %}

Columns 2, 3, and 4 can be selected as pivot columns, for this example column 4 is selected. The values of z resulting from the choice of rows 2 and 3 as pivot rows are 10/1 = 10 and 15/3 = 5 respectively. Of these the minimum is 5, so row 3 must be the pivot row. Performing the pivot produces

{% highlight js %}
|1 -0.66 -3.66 0 0 -1.33 -20|
|0 2.33  0.33  0 1 -0.33  5 |
|0 0.66  1.66  1 0  0.3   5 |
{% endhighlight %}

Now columns 4 and 5 represent the non-basic variables z and s and the corresponding basic feasible solution is

{% highlight js %}
x=y=t=0, z=5, s=5
{% endhighlight %}

For the next step, there are no positive entries in the objective row and in fact

{% highlight js %}
z = -20 + 0.66x + 3.66y + 1.33t
{% endhighlight %}

so the minimum value of Z is −20.

## Implementation

### Parse the input

First thing first, we need to parse the input of an html textarea containing our linear problem.

{% highlight html %}
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>zsdawd</title>
    <script src="simplex.js"></script>
  </head>
  <body>
    <textarea id="lpInput" name="name" rows="8" cols="100">
Maximize p = 0.5x + 3y + z + 4w subject to
x + y + z + w <= 40
-2x - y + z + w <= 10
y - w <= 10
    </textarea>
    <br>
    <input type="button" onclick="createTableau('lpInput')" name="name" value="Click Me">
  </body>
</html>
{% endhighlight %}

### Exo 1

Write the function *createTableau*. This function produces a tableau for us to use in the following steps. The following input

{% highlight js %}
Maximize p = 0.5x + 3y + z + 4w subject to
x + y + z + w <= 40
-2x - y + z + w <= 10
y - w <= 10
{% endhighlight %}

produces this tableau

{% highlight js %}
| o  |  x  |  y | x | w |
| 0  | 0.5 |  3 | 1 | 4 | //-> 0.5x + 3y + z + 4w
| 40 |  1  |  1 | 1 | 1 | //-> x + y + z + w
| 10 |  2  | -1 | 1 | 1 | //-> -2x - y + z + w
| 10 |  0  |  1 | 0 | -1| //-> y - w <= 10
{% endhighlight %}


Here's the Tableau datastructure:

{% highlight js %}
function Tableau(linearString){

  this.variables = ??
  this.constraints = ??
  this.objective = ??

  this.rows = this.constraints.length + 1;
  this.columns = this.variables.length + 1;

  this.matrix = [];
  this.matrix[0] = this.objective.toArray(true);
  for(var i = 0; i < this.constantes.length; i++){
    this.matrix[i+1] = this.constantes[i].toArray();
  }

  this.showMatrix = function(){
    for (var i = 0; i < this.matrix.length; i++) {
      console.log(this.matrix[i]);
    }
  }
}
{% endhighlight %}

It contains an array of all the variables used (i.e. x, y, z and so on), the constraints and the objective. The constraint variance is an array of Constraint and the objective is a Constraint.
Here's the Constraint data structure:

{% highlight js %}
function Constraint(variables, coefVariables, op, string, rightHand){

  for(var i = 0; i < variables.length; i++){
    this[variables[i]] = 0.0;
  }

  for(var y = 0; y < coefVariables.length; y++){
    this[coefVariables[y].variable] = parseFloat(coefVariables[y].coefficient);
  }

  this.variables = variables;
  this.op = op;
  this.string = string;
  this.rightHand = parseFloat(rightHand);

  this.toArray = function(reverse){
    var array = [];
    array[0] = this.rightHand;
    for(var i = 0; i < variables.length; i++){
      array[i+1] = (reverse == true) ? this[this.variables[i]] * -1 : this[this.variables[i]];

    }
    return array;
  }
}
{% endhighlight %}

The first task is to implement the functions needed in Tableau to create the variables, constraint and objective from a String. Then, create a new Tableau that we can use for the Simple algorithm.

{% highlight js %}
function createTableau(inputId){

  lpString = document.getElementById(inputId).value.toLowerCase();
  console.log(lpString);

  linearExpression = new Tableau(lpString);

  simplex(linearExpression);
}
{% endhighlight %}

## Add slack variables

*In general, a linear program will not be given in canonical form and an equivalent canonical tableau must be found before the simplex algorithm can start. This can be accomplished by the introduction of artificial variables. Columns of the identity matrix are added as column vectors for these variables. If the b value for a constraint equation is negative, the equation is negated before adding the identity matrix columns. This does not change the set of feasible solutions or the optimal solution, and it ensures that the slack variables will constitute an initial feasible solution. The new tableau is in canonical form but it is not equivalent to the original problem. So a new objective function, equal to the sum of the artificial variables, is introduced and the simplex algorithm is applied to find the minimum; the modified linear program is called the Phase I problem.*

*The simplex algorithm applied to the Phase I problem must terminate with a minimum value for the new objective function since, being the sum of nonnegative variables, its value is bounded below by 0. If the minimum is 0 then the artificial variables can be eliminated from the resulting canonical tableau producing a canonical tableau equivalent to the original problem. The simplex algorithm can then be applied to find the solution; this step is called Phase II. If the minimum is positive then there is no feasible solution for the Phase I problem where the artificial variables are all zero. This implies that the feasible region for the original problem is empty, and so the original problem has no solution.*[^3]

### Exo 2

Concretely, we want a function addSlackVariables doing the following:

{% highlight js %}
for lines i in the tableau's matrix
  for lines j in the tableau's matrix
    tableau's matrix position i, j + tableau.columns -1 = (i==j);
  }
}
tableau.columns += tableau.rows -1;
{% endhighlight %}

and a function check_b_positive checking if the value are greater than 0:

{% highlight js %}
function check_b_positive(tableau) {
  for(i=1; i<tableau.rows; i++){
    if(tableau.matrix[i][0] < 0){
      console.log("aie");
    }
  }
}
{% endhighlight %}

At the end of the addSlackVariables, our matrix has been transformed to:


{% highlight js %}
[0, -0.5, -3, -1, -4]
[40, 1, 1, 1, 1, true, false, false]
[10, 2, -1, 1, 1, false, true, false]
[10, 0, 1, 0, -1, false, false, true]
{% endhighlight %}

which is a canonical tableau. We can begin the simplex algorithm.

### Pivots

*The geometrical operation of moving from a basic feasible solution to an adjacent basic feasible solution is implemented as a pivot operation. First, a nonzero pivot element is selected in a nonbasic column. The row containing this element is multiplied by its reciprocal to change this element to 1, and then multiples of the row are added to the other rows to change the other entries in the column to 0. The result is that, if the pivot element is in row r, then the column becomes the r-th column of the identity matrix. The variable for this column is now a basic variable, replacing the variable which corresponded to the r-th column of the identity matrix before the operation. In effect, the variable corresponding to the pivot column enters the set of basic variables and is called the entering variable, and the variable being replaced leaves the set of basic variables and is called the leaving variable. The tableau is still in canonical form but with the set of basic variables changed by one element.*[^3]

### Exo 3

To create a pivot, we need a pivot column and a pivot line. Here's the pseudocode to select the pivot column

{% highlight js %}
function findPivotColumn(tableau) {
  j, pivot_col = 1
  lowest = tableau's matrix position 0 1
  for columns j in the tableau's matrix
    if tableau's matrix position 0 j < lowest then
      lowest <- tableau's matrix position 0 j
      pivot_col = j

  if lowest is greater than 0
    pivot_col <- -1

  return pivot_col
}
{% endhighlight %}

and the function for selecting the pivot row

{% highlight js %}
function findPivotRow(tab, pivotCol) {
  i, pivotRow = 0
  minRatio = -1

  for rows i in the tableau's matrix
    ratio = tableau's matrix at i 0 / tableau's matrix at i pivotCol
    if  (ratio > 0  AND ratio < minRatio ) OR minRatio < 0
      minRatio = ratio;
      pivotRow = i;


  if minRatio == -1
    pivotRow -1;

  return pivotRow;
}
{% endhighlight %}

and finally the pivot method itself


{% highlight js %}
function pivotOn(tab, row, col) {
  var i, j;
  var pivot;

  pivot = tableau's matrix at row col
  for col j in the tableau's matrix
    tableau's matrix at row j /= pivot

  for row i in the tableau's matrix
    var multiplier = tableau's matrix at i col;
    if i==row
      continue;


    for col j in the tableau's matrix
      tableau's matrix at i j -= tab.matrix[i][j] -= multiplier * tableau's matrix at row j;

}
{% endhighlight %}

## Simplex Method

Here's the simplex method and the createTableau method.

{% highlight js %}
function createTableau(inputId){

  lpString = document.getElementById(inputId).value.toLowerCase();
  console.log(lpString);

  //Checks if we have a minimize or a maximize
  if(!lpString.contains("mini") && !lpString.contains("maxi")){
    alert("This isn't an LP.")
    return;
  }

  linearExpression = new Tableau(lpString);

  console.log(linearExpression.toArray());
  linearExpression.showMatrix();

  simplex(linearExpression);

  return linearExpression;
}

function simplex(tableau){

  addSlackVariables(tableau);
  check_b_positive(tableau);
  console.log("Padded with slack variables");
  tableau.showMatrix();

  for (var i = 0; i < 30; i++) {

    var pivot_col, pivot_row;

    pivot_col = findPivotColumn(tableau);
    if( pivot_col < 0 ) {
      console.log("Found optimal value=A[0,0]="+tableau.matrix[0][0]+" (no negatives in row 0).");
      printOptimalVector(tableau);
      break;
    }

    console.log("Entering variable x"+pivot_col+" to be made basic, so pivot_col="+pivot_col+".");

    pivot_row = findPivotRow(tableau, pivot_col);
    if (pivot_row < 0) {
      console.log("unbounded (no pivot_row)");
      break;
    }
    console.log("Leaving variable x"+pivot_row+", so pivot_row="+pivot_row+".");

    pivotOn(tableau, pivot_row, pivot_col);
    console.log("After pivoting");
    tableau.showMatrix();
    printOptimalVector(tableau);
  }
}
{% endhighlight %}

If everything went well, the console should display the following:

{% highlight js %}
[145, 4, 0, 3, 0, NaN, NaN, NaN]
[15, -0.5, 1, 0, 0, 0.5, -0.5, 0]
[25, 1.5, 0, 1, 1, 0.5, 0.5, 0]
[20, 2, 0, 1, 0, 0, 1, 1]
x1=0
x2=15
x3=0
x4=25
x5=0
x6=0
x7=20
Most negative column in row[0] is col 2 = 0.
Found optimal value=A[0,0]=145 (no negatives in row 0).
x1=0
x2=15
x3=0
x4=25
x5=0
x6=0
x7=20
{% endhighlight %}

Meaning that the maximum value for p is **145**.

# Correction

## Knapsack

The final project is available at https://github.com/MathieuNls/knapsack.js.
The correction of the first exercice can be fetched with:

* For exos 1 and 2: https://github.com/MathieuNls/knapsack.js/commit/f1781ec6f451ea7216d0421cb19dbf7b673899a0
* For exo 3: https://github.com/MathieuNls/knapsack.js/blob/4d284670f52dc1b50ba93b96c793bf6b4ed9d398/knap.js


## Simplex

The final project is available at https://github.com/MathieuNls/simplex.js.
The correction of the first exercice can be fetched with:

{% highlight js %}
git clone https://github.com/MathieuNls/simplex.js
cd simplex.js
git fetch --all
git reset --hard origin/check-lp-input
{% endhighlight %}

For exo 2 and 3:

{% highlight js %}
git reset --hard origin/simplex
{% endhighlight %}
