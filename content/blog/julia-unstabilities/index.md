---
title: Avoiding Julia type-instabilities
date: "2020-08-05T08:18:03.284Z"
description: "Attached NextJournal's link where I explained who I avoided type-instabilities of complex Julia structures"
---

>   I have just made a blog post (check it out [here!](https://nextjournal.com/a/MnAJsqXABEczWaurbczvN?token=Yb9vvfvHagspFJ8EDJvC6L)) with my own experience trying to avoid type-instabilities of Julia structs.

## Type-instability of Parametrized Structs

![julia.png][nextjournal#file#5c09851e-4fbd-4fb1-afbe-1152084be27b]

First create all the data for our struct attributes.

We are going to create singletons of abstract type `Car`.

```julia
abstract type Car end

struct Volvo <: Car end
struct Mazda <: Car end
```

Then consider the `Struct` where we want to store our data. 

So, lets define a struct as

```julia
abstract type GeneralStruct end

struct AA{T} <: GeneralStruct
  vector::Vector{T}
  car::Car
end
```

The basic idea is to test the correct parametrization of complex structs by accessing their attributes. 

In order to do that, we define the necessary functions as:

```julia
function getvector(mystruct::S) where {S <: GeneralStruct}
  mystruct.vector
end

function getcar(mystruct::S) where  {S <: GeneralStruct}
  mystruct.car
end
```

Instantiate our struct with different types

```julia
a = AA([1.,2.,3.], Volvo())
```

```julia
b = AA([1,2,3], Mazda())
```

Each one is parametrized according to its input data. So, lets check for type stability.

```julia
@code_warntype getvector(a)
```

```julia
@code_warntype getcar(a)
```

So there seems to be an issue with how we parametrized the car attributes.

Therefore, we should better work with a new structure that also parametrizes the singletons of type Car as follows:

```julia
struct AB{T, C <: Car} <: GeneralStruct
  vector::Vector{T}
  car::C
end
```

```julia
a = AB([1., 2., 3.], Volvo())
```

This new object has parametrized all the data objects inside `{Float64, Volvo}` , so the compiler nows in advance what kind of objects to expect.

```julia
@code_warntype getcar(a)
```

Now everything seems to be working fine.

The next step is try to make a collection with these structs, i.e., a **dictionary** or **tuples**. Let's see the difference.

```julia
aa = Dict{Symbol,T where T <: GeneralStruct}(:a=> a, :b=> b)
```

```julia 
bb = (; :a => a, :b => b)
```

`Dictionaries` in this case doesn't seem to parametrize correctly these objects whereas for the `NamedTuple` created this problem is not present.  Let's check this with an example.

First define a function that retrieves an element from it of type `GeneralStruct`. 

```julia 
function getfroma(a::Dict)
    a[:b]
end
function getfroma(a::NamedTuple)
    a[end]
end
```

```julia 
@code_warntype getfroma(aa)
```

```julia 
@code_warntype getfroma(bb)
```

Clearly the dictionary doesn't parametrize correctly the object inside, whereas for the named tuple it works correclty.

```javascript{numberLines: true}
var s = "JavaScript syntax highlighting";
alert(s);
```

```python
s = "Python syntax highlighting"
print s
```

[nextjournal#file#5c09851e-4fbd-4fb1-afbe-1152084be27b]:
<https://nextjournal.com/data/QmT5fDkSq8GZVpJovSHAxvUHBpDYvcGSe16GKJfAWDawZJ?filename=julia.png&content-type=image/png>

<details id="com.nextjournal.article">
<summary>This notebook was exported from <a href="https://nextjournal.com/a/MnAJsqXABEczWaurbczvN?change-id=CkbCKBgBNQuXc3dC8YxB3G">https://nextjournal.com/a/MnAJsqXABEczWaurbczvN?change-id=CkbCKBgBNQuXc3dC8YxB3G</a></summary>

</details>
