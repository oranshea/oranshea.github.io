---
title:  How to simplify a fraction in cpp
date:   2026-09-21
tag: [math, cpp]
math: true
published: true
---

# Simplifying a Fraction

How do we represent a fraction in its simplest form in C++?

Suppose we are given two integers, `a` and `b`, and we want to
represent

$$
\frac{a}{b}
$$

in its simplest form. Since we don't know what `a` and `b` are in
advance, we need a general method to reduce the fraction.

Fortunately, there is a well-known algorithm called the [Euclidean
algorithm](https://en.wikipedia.org/wiki/Euclidean_algorithm), which can
be used to find the **Greatest Common Divisor (GCD)** of two integers.

## The Euclidean Algorithm

The key property of the Euclidean algorithm is:

$$
\gcd(a,b)=\gcd(b,a\bmod b)
$$

The algorithm repeatedly replaces `(a, b)` with `(b, a mod b)` until
`b = 0`.

For example:

$$
\begin{aligned}
\gcd(24,18)
&=\gcd(18,6)\\
&=\gcd(6,0)\\
&=6
\end{aligned}
$$

We can implement it recursively in C++:

``` cpp
int gcd(int a, int b) {
return b == 0 ? a : gcd(b, a % b);
}
```

## Simplifying the Fraction

Once we know the GCD, obtaining the simplest fraction is
straightforward.

We divide both the numerator and denominator by the GCD:

$$
\frac{a}{b}
=
\frac{a/\gcd(a,b)}{b/\gcd(a,b)}
$$

For example:

$$
\frac{24}{18}
=
\frac{24/6}{18/6}
=
\frac{4}{3}
$$

In C++, we can write:

``` cpp
int a, b;
cin >> a >> b;

int g = gcd(a, b);

a /= g;
b /= g;

cout << a << "/" << b;
```

The important idea here is that we don't need to know $`a`$ and $`b`$
beforehand. As long as we can calculate their GCD, we can always reduce
the fraction to its simplest form.

## Negative Numbers

If `a` or `b` can be negative, we should also consider the sign of
the fraction.

By convention, it is usually better to keep the denominator positive.

For example:

$$
\frac{3}{-4}=-\frac{3}{4}
$$

So we can normalize the sign after reducing the fraction:

``` cpp
if (b < 0) {
a = -a;
b = -b;
}
```

This gives us a consistent representation of the fraction.
