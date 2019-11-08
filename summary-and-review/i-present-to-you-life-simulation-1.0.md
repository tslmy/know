# I present to you, life simulation 1.0

I present to you, _life simulation 1.0_.

First, initialize an object with optional parameters. All arguments, including `bankSavings`, are optional and have reasonable default values.

```python
>>> life_simulation = LifeSimulation(startAge = 18)
```

`objFn` is the _objective function_ to maximize:

```python
>>> life_simulation.run(objFn = lambda state: 
        state.time.with(state.relationships.loved_ones))
Simulating life starting at age 18...
---------------
Died at 18.01 year(s) old due to <PhysicalError: Starvation>.
Traceback:
  PhysicalError: Starvation
```

Oops, we spent too much time with our parents and significant other that we forgot to eat! We need to remember eat and drink. Let's schedule that periodically:

```python
>>> life_simulation.run(objFn = lambda state: 
        state.time.with(state.relationships.loved_ones),
        schedule = {every('8h'): eatAndDrink})
Simulating life starting at age 18...
---------------
Died at 18.3 year(s) old due to <PhysicalError: Starvation>.
Traceback:
  PhysicalError: Starvation
   ↖FinancialError: Bankrupt
```

Turns out spending time eating and drinking with your loved ones without income is not very sustainable. Let's get employed and get paid:

```python
>>> life_simulation.run(objFn = lambda state: 
        state.time.with(state.relationships.loved_ones),
        schedule = {every('8h'): eatAndDrink,
                    every('1d'): work,
                    now  ()    : jobHunt})
Simulating life starting at age 18...
---------------
Warning: `jobHunt` failed due to <SocialError: Insufficient education>.
Died at 18.3 year(s) old due to <PhysicalError: Starvation>.
Traceback:
  PhysicalError: Starvation
   ↖FinancialError: Bankrupt
```

Bummers. Let's fix that real quick \(error message trimmed with `<...>`\):

```python
>>> life_simulation.run(objFn = lambda state: 
        state.time.with(state.relationships.loved_ones),
        schedule = {every('8h'): eatAndDrink,
                    every('1d'): work,
                    now  ()    : {'do': goSchool, 
                                  'callback': jobHunt}})
Simulating life starting at age 18...
---------------
Warning: `goSchool` failed due to <FinancialError: Insufficient fund>.
Warning: `jobHunt` <...>
```

This is getting frustrating. Let's cheat a bit.

```python
life_simulation = LifeSimulation(startAge = 18, bankSavings = 100000)
```

Now this \(finally\) works as expected:

```python
>>> %%
Simulating life starting at age 18...
---------------
21.7 year(s) old: <PhysicalWarning:Fatigue>
24.3 year(s) old: <PhysicalWarning:Fatigue>
25.6 year(s) old: <PhysicalWarning:Fatigue>
25.8 year(s) old: <PhysicalWarning:Fatigue>
...(96 warning(s) omitted)
Died at 26 year(s) old due to <PhysicalError: Heart attack>.
Traceback:
  PhysicalError: Heart attack
   ↖PhysicalWarning:Fatigue
```

Hooray! We got 8 years more out of our \(simulated\) life. In the next tutorial, I will demonstrate how holidays and vacations are implemented to extend our lifespan even further.

Hope you enjoyed this tutorial. Remember to take good care of your real life.

