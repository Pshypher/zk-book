# Chapter 2: Finite Fields and Modular Arithmetic

## Exercise 1

###### Let’s say we pick a p >= 3. Which, if any, non-zero values are their own additive inverse?

The non-zero values say _**x**_ in the finite-field _**(mod p)**_ have their additive inverse expressed as _**p + (-x) == p - x**_

## Exercise 2

###### Find the multiplicative inverse of 3 modulo 5. There are only 5 possibilities, so try all of them and see which ones work.

_(3)(3<sup>p - 2</sup>) == 1 (mod p)_

_p = 5_

_(3)(3<sup>5 - 2</sup>) == 1 (mod 5)_

_3<sup>5 - 2</sup> == 3<sup>3</sup> (mod 5)_

_3<sup>3</sup> (mod 5) == 2 (mod 5)_


## Exercise 3

###### What is the multiplicative inverse of 50 in the finite field p = 51? You do not need Python to compute this, see the principles described in “General rules of multiplicative inverses.

_p = 51 &  p - 1 = 50_

The multiplicative inverse for _(p - 1)_ is itself _(p - 1)_

## Exercise 4

###### Use Python to compute the multiplicative inverse of 288 in the finite field of p = 311. You can check your work by validating that (288 * answer) % 311 == 1.

```python
print(pow(288, -1, 311) 
```

## Exercise 5

###### Run pow(7, -1, 7) in Python. You should see an exception get thrown, ValueError: base is not invertible for the given modulus.

```python
>>> pow(7, -1, 7)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: base is not invertible for the given modulus
```

## Exercise 6

###### Check that 3/4 * 1/2 = 3/8 in the finite field p = 17.

```python
import galois
GF17 = galois.GF(17)
three_quarter = GF17(3) / GF17(4)
one_half = GF17(1) / GF17(2)
three_eighth = GF17(3) / GF17(8)
assert one_half * three_quarter == three_eighth
```

## Exercise 7

###### Verify the claimed square roots in the table are correct in the finite field modulo 11.

```python
numbers_with_roots = dict()
p = 11
for i in range(0, p):
...     key = i * i % p
...     if key in numbers_with_roots:
...             numbers_with_roots[key].add(i)
...     else:
...             numbers_with_roots[key] = set()
...             numbers_with_roots[key].add(i)
```

## Exercise 8

```python
def mod_sqrt(x, p):
    assert (p - 3) % 4 == 0, "prime cannot be expressed as a result of 4k + 3"
    exponent = (p + 1) // 4
    return pow(x, exponent, p) # x ^ e % p
```

###### Use the code snippet above to compute the modular square root of 5 in the finite field of p = 23. The code will only give you one of the answers. How can you compute the other?

```python
p = 23
first_root = mod_sqrt(5, p)
second_root = p - first_root
```

## Exercise 9

###### Write code to bruteforce every combination of (x, y) over x = 0..10, y = 0..10 to verify the above system has no solution over the finite field of p = 11.

```python
import galois
p = 11
GF = galois.GF(p)
one_half = GF(1) / GF(2)
two_third = GF(2) / GF(3)
seven_third = GF(7) / GF(3)
pairs = []
for x in range(0, p):
    y1 = one_half - one_half * GF(x)
    y2 = two_third - seven_third * GF(x)
    print("[(", x, ",", y1, "), (", x, ",", y2, ")]", sep = "", end = " ")
    
 print()
```
## Exercise 10

> _x + 2y = 3_
>
> _4x + 8y = 1_

###### Convert the two equations to their finite field representation and see they are the same.

> _y = 1/2 * 3 - 1/2 * x_
>
> _y = 1/8 - 1/2 * x_

> _y = (inv(2) * 3 - inv(2) * x) mod(11)_ 
> 
> _y = (inv(8) - inv(2) * x) mod(11)_

> _y = (6 * 3) mod(11) - 6x_
>
> _y = 7 - 6x_

> _y = 7 - 6x_
> 
> _y = 7 - 6x_

# Practice Problems

###### In the problems below, use a finite field p of 21888242871839275222246405745257275088548364400416034343698204186575808495617. Beware that the galois library takes a while to initialize a GF object, galois.GF(p), of this size.

## Exercise 1

###### A dev creates an arithmetic circuit x * y * z === 0 and x + y + z === 0 with the intent of constraining all the signals to be zero. Find a counter example to this where the constraints are satisfied, but not all of x, y, and z are 0.

```python
import galois
p = 21888242871839275222246405745257275088548364400416034343698204186575808495617
GF = galois.GF(p)
for i in range(1, p):
    for j in range(1, p):
        for k in range(1, p):
            x = GF(i); y = GF(j); z = GF(k)
                if (x + y + z == 0  and x * y * z == 0 and not(x == 0 and y == 0 and z == 0)):
                    print(x, y, z)
```
A valid counter example is _**x = 0, y = p - 1, z = 1**_.

> _**x + y + z === 0 + (p - 1) + 1 (mod p) === 0 + p (mod p) === p (mod p) === 0**_
> 
> _**x * y * z === 0 * (p - 1) * 1 === 0**_

## Exercise 2


###### A dev creates a circuit with the polynomial x² + 2x + 3 === 11 and proves that 2 is a solution. What is the other solution? Hint: write the circuit as x² + 2x - 8 === 0 then factor the polynomial by hand to find the roots. Finally, compute the congruent element of the roots in the finite field to find the other solution.

Solving by hand

> _x<sup>2</sup> + 2x - 8 == (x - 2)(x + 4)_

> _x = 2; x = -4_

> _-4 (mod p) = p + (-4)_
> 
> _21888242871839275222246405745257275088548364400416034343698204186575808495617 - 4 = 21888242871839275222246405745257275088548364400416034343698204186575808495613_