## Download & install Anaconda

![graph](1.png)

### Part 2: `health_agents.py` — 20 Marks

In the file `health_agents.py` there is a class called `HealthAgent`. This defines an agent which, very poorly, attempts to control the spread of disease. In each step of the simulation, it will move to the adjacent location with the most disease. If no adjacent locations have any disease, it will move randomly.

You should extend `HealthAgent` with your own agent class called `SmartHealthAgent` and implement an appropriate `choose_move` method. Note that your `choose_move` method must have the same parameters as that in `HealthAgent` (i.e. you cannot add extra parameters)

Feel free to add other helper methods and classes if needed.

Test your agent with the scenarios in the `exercise4_maps` subdirectory.

Whenever the simulator is not run in Testing mode, a file called `XXXX.results.json` is created. It contains a summary of the outcomes of the simulations in a JSON document. For each run of the simulator the level of final disease, number of simulation steps and score are stored. You will also see that the average_score is also available.

Run `python3 disease_simulation.py` to find out how to run several simulations. Do not edit or submit the `disease_simulation.py` file.

The number of marks you get in this exercise depends on how good the performance of your agent is compared to that of `HealthAgent` over the five given scenarios. It is not necessary to eradicate all diseases in all places to get full marks. We will use the following parameters to evaluate your agent:

```
-H 100 -n 100
```

that is, over 100 simulation runs, each run with a maximum of 100 steps. The algorithm should run fast. If it takes more than a few seconds to run all simulations, try a simpler approach.

Don't forget that you need to comment your code to explain which algorithm you're using and/or how it works.

## Useful Things

The following sections of this tutorial are non-compulsory, but they introduce some powerful features of Python, which might make your life a lot easier, so it is recommended that you read them some time.

### The itertools Module

The `itertools` module contains a set of powerful functions to deal with iterators. They can save you a lot of time and effort.

A thorough overview of the module can be found [here](https://docs.python.org/3/library/itertools.html).

We will cover just a few examples here.

First, `itertools.chain` provides an easy way to combine multiple iterators into a single iterator:

```python
>>> import itertools
>>> x = range(1, 3)
>>> for item in itertools.chain(range(5, 7), x, range(11, 13)):
        print(item)
5
6
1
2
11
12
```

Next, `itertools.combinations` can generate all (unordered) combinations of a given size from elements in an iterator:

```python
>>> list(itertools.combinations("abcd", 3))
[('a', 'b', 'c'), ('a', 'b', 'd'), ('a', 'c', 'd'), ('b', 'c', 'd')]
```

Next, `itertools.product` can generate Cartesian products from a list of iterators:

```python
>>> x = [[True, False]] * 3
>>> x
[[True, False], [True, False], [True, False]]
>>> list(itertools.product(*x))
[(True, True, True),
 (True, True, False),
 (True, False, True),
 (True, False, False),
 (False, True, True),
 (False, True, False),
 (False, False, True),
 (False, False, False)]
```

Here, the `*` before `x` in the call to `itertools.product` unpacks the elements of `x` into the arguments of `itertools.product`. It is equivalent to calling the function with three lists of the form `[True, False]`.

This final call would have been helpful in Exercise 2.

### Comprehensions — Or how much can I do in one statement?

You may have noticed that Python is a very compact language. It is not uncommon to feel a sense of exhilaration when you realise that you can solve problems often with a small fraction of the number of lines of code that would be required in C++ or Java.

Lets take this even further and put a for loop inside the definition of a list.

```python
>>> [x ** 2 for x in range(10)]
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

What about making a dictionary which maps the letters of the alphabet to their position in the alphabet?

```python
>>> alph_index = dict([(a,  i) for i, a in enumerate("abcdefghijklmnopqrstuvwxyz")])
>>> alph_index["j"]
10
>>> alph_index["z"]
25
```

We can nest loops and even add conditionals. What if want a list of all coordinate pairs in a grid, except those points on the diagonal?

```python
>>> [(x, y) for x in range(5) for y in range(5) if x != y]
[(0, 1),
 (0, 2),
 (0, 3),
 (0, 4),
 (1, 0),
 (1, 2),
 ...
```

It is easy to go overboard with list comprehensions and make your code hard to read. So keep them simple!

Having said that, it might be a fun exercise at this point to think about how to use a list comprehension to compute all prime numbers up to a given bound.

And that's the end of Assignment 0 :-)
