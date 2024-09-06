# Chapter 2: Arithmetic Circuits

## Exercise 1

###### Create an arithmetic circuit that takes signals x₁, x₂, ..., xₙ and is satisfied if at least one signal is 0.

**Constraints**

> _x<sub>1</sub> . (x<sub>1</sub> - 1) === 0_
>
> _x<sub>2</sub> . (x<sub>2</sub> - 1) === 0_
>
> **_..._**
>
> _x<sub>n</sub> . (x<sub>n</sub> - 1) === 0_


**Arithmetic Circuit**

> _out === 1 - (x<sub>1</sub>.x<sub>2</sub> ... x<sub>n-1</sub>.x<sub>n</sub>)_

## Exercise 2

###### Create an arithmetic circuit that takes signals x₁, x₂, ..., xₙ and is satisfied if all are 1.

**Constraints**

> _x<sub>1</sub> . (x<sub>1</sub> - 1) === 0_
>
> _x<sub>2</sub> . (x<sub>2</sub> - 1) === 0_
>
> **_..._**
>
> _x<sub>n</sub> . (x<sub>n</sub> - 1) === 0_


**Arithmetic Circuit**

> _out === x<sub>1</sub> * x<sub>2</sub> * ... * x<sub>n</sub>_

## Exercise 3

###### A bipartite graph is a graph that can be colored with two colors such that no two neighboring nodes share the same color. Devise an arithmetic circuit scheme to show you have a valid witness of a 2-coloring of a graph. Hint: the scheme in this tutorial needs to be adjusted before it will work with a 2-coloring.

**Constraints**

For a bipartite graph we employ 2 colors where red = 1 and blue = 2.

> _(x - 1)(x - 2) === 0_
> 
> _(y - 1)(y - 2) === 0_

**Arithmetic Circuit**
> _0 === 2 - (x)(y)_

## Exercise 4

###### Devise an arithmetic circuit that constrains k to be the maximum of x, y, or z. That is, k should be equal to x if x is the maximum value, and same for y and z.

**Constraints**

> _(k - x)(k - y)(k - z) === 0_

**Arithmetic Circuit**

_k_ and _m_ is represented with at most n - 1 bits, where _m_ is one of (_x_, _y_, _z_)

> _2<sup>n - 2</sup>k<sub>n - 2</sub> + ... +  2<sup>1</sup>k<sub>1</sub> + 2<sup>0</sup>k<sub>0</sub> === k_
> 
> _2<sup>n - 2</sup>m<sub>2</sub> + ... + 2<sup>1</sup>m<sub>1</sub> + 2<sup>0</sup>m<sub>0</sub> === m_
> 
> _k<sub>n - 2</sub>(k<sub>n - 2</sub> - 1) === 0_
> 
> **...**
> 
> _k<sub>1</sub>(k<sub>1</sub> - 1) === 0_
> 
> _k<sub>0</sub>(k<sub>0</sub> - 1) === 0_
> 
> _m<sub>n - 2</sub>(m<sub>n - 2</sub> - 1) === 0_
> 
> **...**
> 
> _m<sub>1</sub>(m<sub>1</sub> - 1) === 0_
> 
> _m<sub>0</sub>(m<sub>0</sub> - 1) === 0_
> 
> _2<sup>n - 1</sup> + (k - m) === 2<sup>n - 1</sup>q<sub>n - 1</sub> + ... + 2<sup>2</sup>q<sub>2</sub> + 2<sup>1</sup>q<sub>1</sub> + 2<sup>0</sup>q<sub>0</sub>_ 

Check that the MSB is 1
> _q<sub>n - 1</sub> === 1_

We substitute x, y, and z for m in the **[Arithmetic Circuit](#exercise-4)** above and compare it against _k_ to assert that k is the maximum of (_x, y, z_)

## Exercise 5

###### Create an arithmetic circuit that takes signals x₁, x₂, ..., xₙ, constrains them to be binary, and outputs 1 if at least one of the signals is 1. Hint: this is tricker than it looks. Consider combining what you learned in the first two problems and using the NOT gate.

**Constraints**

> _x<sub>1</sub> . (x<sub>1</sub> - 1) === 0_
>
> _x<sub>2</sub> . (x<sub>2</sub> - 1) === 0_
>
> **_..._**
>
> _x<sub>n</sub> . (x<sub>n</sub> - 1) === 0_

**Arithmetic Circuit**

> _out === (x<sub>1</sub> + x<sub>2</sub> + ... + x<sub>n</sub>) - (x<sub>1</sub>.x<sub>2</sub> + ... + x<sub>2</sub>.x<sub>n</sub>) + (-1)<sup>n-1</sup>(x<sub>1</sub>.x<sub>2</sub>.x<sub>n</sub>)_

## Exercise 6

###### Devise an arithmetic circuit to determine if a signal v is a power of two (1, 2, 4, 8, etc). Hint: create an arithmetic circuit that constrains another set of signals to encode the binary representation of v, then place additional restrictions on those signals.

**Constraints**

> _b<sub>0</sub> . (b<sub>0</sub> - 1) === 0_
>
> _b<sub>1</sub> . (b<sub>1</sub> - 1) === 0_
>
> **_..._**
>
> _b<sub>n - 1</sub> . (b<sub>n - 1</sub> - 1) === 0_

**Arithmetic Circuit**

> _out === 2<sup>n - 1</sup>b<sub>n - 1</sub> + ... + 2<sup>1</sup>b<sub>1</sub> + 2<sup>0</sup>b<sub>0</sub>_
> 
> _b<sub>n - 1</sub> === 1_
> 
> _b<sub>n - 2</sub> === 0_
> 
> **...**
> 
> 
> _b<sub>1</sub> === 0_
> 
> _b<sub>0</sub> === 0_

## Exercise 7

###### The covering set problem starts with a set S = {1, 2, …, 10} and several well-defined subsets of S, for example: {1, 2, 3}, {3, 5, 7, 9}, {8, 10}, {5, 6, 7, 8}, {2, 4, 6, 8}, and asks if we can take at most k subsets of S such that their union is S. In the example problem above, the answer for k = 4 is true because we can use {1, 2, 3}, {3, 5, 7, 9}, {8, 10}, {2, 4, 6, 8}. Note that for each problems, the subsets we can work with are determined at the beginning. We cannot construct the subsets ourselves. If we had been given the subsets {1,2,3}, {4,5} {7,8,9,10} then there would be no solution because the number 6 is not in the subsets.On the other hand, if we had been given S = {1,2,3,4,5} and the subsets {1}, {1,2}, {3, 4}, {1, 4, 5} and asked can it be covered with k = 2 subsets, then there would be no solution. However, if k = 3 then a valid solution would be {1, 2}, {3, 4}, {1, 4, 5}. Our goal is to prove for a given set S and a defined list of subsets of S, if we can pick a set of subsets such that their union is S. Specifically, the question is if we can do it with k or fewer subsets. We wish to prove we know which k (or fewer) subsets to use by encoding the problem as an arithmetic circuit.

**Steps**

1. Choose a combination of _k_ subsets from the given list of subsets.
2. Merge the elements from the subsets into a single set i.e find the union _U_ of the chosen _k_ subsets.
3. Given _S = {1, 2, 3, ..., n}_ check if the union of the chosen subsets in [2]() above is the same as _S_.
4. We use the arithmetic circuit below to determine if the union of the subsets in [2]() is similar to _S_.


**Arithmetic Circuit**

> _(a - 1)(a - 2)...(a - n) + (b - 1)(b - 2)...(b - n) + ... + (n - 1)(n - 2)...(n - n)_ === 0
