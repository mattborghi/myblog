---
layout: post
title: Avoiding Allocations
image: ../julia-unstabilities/juliab.jpeg
author: [Matias Borghi]
date: 2020-08-05T08:18:03.284Z
excerpt: JuliaCon 2020 Avoiding Allocations lecture
tags: ['Julia']
---

## Avoiding Allocations

I found quite interesting this talk at the JuliaCon 2020 so I made a quick compilation of it below.

<iframe width="560" height="315" src="https://www.youtube.com/embed/o8qTJGcPWkE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

> _Tips & tricks_:

* Use [**StaticArrays**](https://github.com/JuliaArrays/StaticArrays.jl).

    - SArray (less than 14x14, Stack-allocated)
    - MArray (less than 14x14, Heap-allocated)
    - SizedArray (any size, wrapper around Array).

* Use [**Function Barriers**](https://docs.julialang.org/en/v1/manual/performance-tips/#:~:text=Separate%20kernel%20functions%20(aka%2C%20function%20barriers),-Many%20functions%20follow&text=Julia's%20compiler%20specializes%20code%20for,since%20it%20is%20chosen%20randomly).

* Use **Vectors of Arrays** rather than increasing dimension and doing slicing.