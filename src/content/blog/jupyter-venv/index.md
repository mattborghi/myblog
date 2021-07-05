---
layout: post
title: Launching Jupyter Notebook inside a Virtual Environment
image: ../../img/computer.jpg
author: [Matias Borghi]
date: 2021-07-05
excerpt: Useful commands used for launching Jupyter Notebooks inside a Virtual Environment
tags:
    - 'Computing'
    - 'Virtual Environment'
    - 'Jupyter Notebook'
---

The first step is creating the virtual environment that has all the packages. 

```shellsession
$ mkdir myproject && cd myproject
$ python -m venv env 
$ source venv/bin/activate 
```

Install `ipykernel` and create a new one for our virtual environment

```shellsession
(env) $ python -m pip install ipykernel
(env) $ ipython kernel install --user --name=<REPLACE-WITH-KERNEL-NAME>
```

Finally, lunch jupyter and check it was created

```shellsession
(env) $ jupyter notebook
```

> In order to do the same in Julia follow [these](https://julialang.github.io/IJulia.jl/stable/manual/installation/#Installing-additional-Julia-kernels) steps.

## Removing Kernels

Run `jupyter kernelspec list` to get the name of all your kernels.

Then simply uninstall your `<KERNEL-NAME>`

```shellsession
jupyter kernelspec uninstall <KERNEL-NAME>
```