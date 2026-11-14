# Number Theory and Cryptography Workshop

**Name:** Joy Karmoker  
**Student ID:** IT23014 
**Workshop:** Introduction to Number Theory and Cryptography  
**Reference Repository:** [mnp-club/Number_Theory_and_Cryptography_Workshop](https://github.com/mnp-club/Number_Theory_and_Cryptography_Workshop)

---

## 1. Introduction

This repository contains my practical work and Python implementations from the **Number Theory and Cryptography Workshop**.

The main objective of this practice was to understand fundamental number theory concepts and implement their algorithms using Python. I practiced mathematical problems involving the Greatest Common Divisor (GCD), Extended Euclidean Algorithm, Least Common Multiple (LCM), Diophantine Equations, Modular Arithmetic, Modular Inverse, Fast Modular Exponentiation, and the Chinese Remainder Theorem.

I implemented the algorithms independently and tested them using different input values in a Python environment.

## 2. Objectives

- Understand the fundamental concepts of number theory.
- Implement the Euclidean Algorithm and Extended Euclidean Algorithm.
- Calculate GCD and LCM efficiently.
- Solve linear Diophantine equations.
- Understand modular arithmetic and multiplicative inverses.
- Implement fast modular exponentiation.
- Apply the Chinese Remainder Theorem to solve simultaneous congruences.
- Improve problem-solving and algorithmic programming skills using Python.

## 3. Tools and Technologies

| Tool / Technology | Purpose |
|---|---|
| Python 3 | Algorithm implementation |
| Google Colab | Online Python practice |
| Jupyter Notebook | Interactive coding and testing |
| GitHub | Source code management and submission |
| Markdown | Documentation |

## 4. Practical Implementations

### Problem 1: Extended Euclidean Algorithm

**Objective:** Implement the Extended Euclidean Algorithm to calculate the GCD of two integers and find two coefficients, x and y, satisfying Bézout's identity.

**Mathematical Equation:**

\[
ax+by=\gcd(a,b)
\]

**Python Implementation:**

```python
def extended_gcd(a, b):
    assert a >= b and b >= 0 and a + b > 0

    if b == 0:
        d, x, y = a, 1, 0
    else:
        d, x1, y1 = extended_gcd(b, a % b)
        x = y1
        y = x1 - (a // b) * y1

    assert a % d == 0 and b % d == 0
    assert d == a * x + b * y

    return (d, x, y)


print(extended_gcd(8, 4))
print(extended_gcd(27, 15))
```

**Output:**

```text
(4, 0, 1)
(3, -1, 2)
```

**Learning Outcome:** Learned how to calculate GCD and determine integer coefficients using the Extended Euclidean Algorithm.

---

### Problem 2: Least Common Multiple (LCM)

**Objective:** Implement an efficient algorithm to calculate the LCM of two integers using the relationship between GCD and LCM.

**Mathematical Equation:**

\[
LCM(a,b)=\frac{|a\times b|}{GCD(a,b)}
\]

**Python Implementation:**

```python
def lcm(a, b):
    x, y = a, b

    while y != 0:
        x, y = y, x % y

    gcd = x

    return abs(a * b) // gcd


print(lcm(9, 3))
print(lcm(17, 37))
```

**Output:**

```text
9
629
```

**Learning Outcome:** Understood how GCD can be used to calculate LCM efficiently.

---

### Problem 3: Solving Diophantine Equations

**Objective:** Use the Extended Euclidean Algorithm to solve linear Diophantine equations.

**Mathematical Equation:**

\[
ax+by=c
\]

A solution exists if:

\[
GCD(a,b)\mid c
\]

**Python Implementation:**

```python
def diophantine(a, b, c):
    if a >= b:
        gcd, x1, y1 = extended_gcd(a, b)
    else:
        gcd, y1, x1 = extended_gcd(b, a)

    assert c % gcd == 0

    factor = c // gcd

    x = x1 * factor
    y = y1 * factor

    assert a * x + b * y == c

    return (x, y)


print(diophantine(34, 51, 170))
print(diophantine(91, 117, 65))
```

**Output:**

```text
(2, 2)
(20, -15)
```

**Learning Outcome:** Learned how to find integer solutions of linear Diophantine equations using the Extended Euclidean Algorithm.

---

### Problem 4: Modular Inverse and Modular Division

**Objective:** Implement an efficient algorithm to calculate the multiplicative inverse of an integer modulo n and perform modular division.

**Mathematical Equation:**

The modular inverse satisfies:

\[
a\times a^{-1}\equiv1\pmod n
\]

It exists when:

\[
GCD(a,n)=1
\]

Modular division is calculated as:

\[
b/a\pmod n = (b\times a^{-1})\bmod n
\]

**Python Implementation:**

```python
def modInverse(a, n):
    if a >= n:
        gcd, x, y = extended_gcd(a, n)
    else:
        gcd, y, x = extended_gcd(n, a)

    assert gcd == 1

    return x % n


def divide(b, a, n):
    assert n > 1 and a > 0

    aInv = modInverse(a, n)

    assert (a * aInv) % n == 1

    return (aInv * b) % n


print(divide(9, 5, 3))
print(divide(223, 67, 54))
```

**Output:**

```text
0
13
```

**Learning Outcome:** Understood multiplicative modular inverses and how they are used to perform modular division.

---

### Problem 5: Fast Modular Exponentiation

**Objective:** Implement Fast Modular Exponentiation using the Square-and-Multiply algorithm without using Python's built-in exponentiation functions.

**Mathematical Equation:**

\[
Result=b^e\bmod m
\]

The algorithm uses repeated squaring to reduce the number of modular multiplications.

**Python Implementation:**

```python
def FastModularExponentiation(b, e, m):
    result = 1
    b = b % m

    while e > 0:
        if e % 2 == 1:
            result = (result * b) % m

        b = (b * b) % m
        e = e // 2

    return result


print(FastModularExponentiation(4, 5, 3))
```

**Output:**

```text
1
```

**Time Complexity:**

\[
O(\log e)
\]

**Learning Outcome:** Learned how repeated squaring makes modular exponentiation faster and more efficient.

---

### Problem 6: Chinese Remainder Theorem (CRT)

**Objective:** Implement the Chinese Remainder Theorem to find a number satisfying two simultaneous modular congruences.

**Mathematical Equations:**

Given:

\[
x\equiv r_1\pmod{n_1}
\]

\[
x\equiv r_2\pmod{n_2}
\]

Where:

\[
GCD(n_1,n_2)=1
\]

Using Extended Euclidean Algorithm:

\[
n_1u+n_2v=1
\]

The solution can be calculated using:

\[
k=(r_2-r_1)u\bmod n_2
\]

\[
x=(r_1+n_1k)\bmod(n_1n_2)
\]

**Python Implementation:**

```python
def ChineseRemainderTheorem(n1, r1, n2, r2):

    if n1 >= n2:
        d, x, y = extended_gcd(n1, n2)
    else:
        d, y, x = extended_gcd(n2, n1)

    assert d == 1

    k = ((r2 - r1) * x) % n2

    result = (r1 + n1 * k) % (n1 * n2)

    return result


print(ChineseRemainderTheorem(13, 7, 6, 5))
print(ChineseRemainderTheorem(28, 20, 19, 3))
```

**Output:**

```text
59
440
```

**Learning Outcome:** Learned how to combine multiple modular congruences into a single solution using CRT.

---

## 5. Summary of Practical Problems

| No. | Topic | Main Algorithm |
|---|---|---|
| 1 | Extended Euclidean Algorithm | Recursive Euclidean Algorithm |
| 2 | Least Common Multiple | GCD-based calculation |
| 3 | Diophantine Equations | Extended Euclidean Algorithm |
| 4 | Modular Inverse and Division | Extended Euclidean Algorithm |
| 5 | Fast Modular Exponentiation | Square-and-Multiply |
| 6 | Chinese Remainder Theorem | Extended GCD and modular arithmetic |

## 6. Key Learning Outcomes

Through these practical exercises, I gained hands-on experience with:

- Understanding the relationship between GCD and LCM.
- Finding Bézout coefficients using the Extended Euclidean Algorithm.
- Solving linear Diophantine equations.
- Calculating modular multiplicative inverses.
- Performing modular division.
- Implementing efficient modular exponentiation.
- Solving simultaneous congruences using the Chinese Remainder Theorem.
- Improving Python programming and mathematical problem-solving skills.

I also learned that several number theory algorithms are closely connected and can be reused to solve more complex mathematical problems.

## 7. Applications in Cryptography

The concepts practiced in this workshop are important foundations of modern cryptography.

Some applications include:

1. **RSA Encryption:** Uses modular exponentiation and modular inverses.
2. **Public-Key Cryptography:** Relies on modular arithmetic and number theory.
3. **Cryptographic Key Generation:** Uses prime numbers, GCD, and modular arithmetic.
4. **Chinese Remainder Theorem:** Can optimize modular computations in RSA implementations.
5. **Efficient Computation:** Fast modular exponentiation reduces computational complexity.

## 8. Repository Structure

My repository is organized as follows:

```text
Number-Theory-and-Cryptography/
│
├── README.md
│
├── Number_Theory_Workshop.ipynb
│
├── codes/
│   ├── extended_gcd.py
│   ├── lcm.py
│   ├── diophantine.py
│   ├── modular_inverse.py
│   ├── fast_modular_exponentiation.py
│   └── chinese_remainder_theorem.py
│
└── figures/
    └── algorithm_flowchart.png
```

## 9. Conclusion

This workshop provided practical experience in implementing fundamental number theory algorithms using Python. By solving the six programming problems, I developed a better understanding of the Extended Euclidean Algorithm, modular arithmetic, Diophantine equations, fast modular exponentiation, and the Chinese Remainder Theorem.

The exercises helped me connect mathematical concepts with programming implementations and understand their importance in cryptography and computer security.

Overall, this practice strengthened my mathematical reasoning, algorithm design, and Python programming skills.

## 10. References

1. [Introduction to Number Theory and Cryptography Workshop – Official GitHub Repository](https://github.com/mnp-club/Number_Theory_and_Cryptography_Workshop)
2. [Python Official Documentation](https://docs.python.org/3/)
3. [Google Colab](https://colab.research.google.com/)
4. [Jupyter Notebook Documentation](https://jupyter-notebook.readthedocs.io/)

---

**Submitted as practical work for the Number Theory and Cryptography Workshop.**
