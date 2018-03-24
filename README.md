
# Conditionals

### Introduction

So far, we have seen how retrieve data from our code, and manipulate that data.  What we have not learned, however, is how to make decisions with that data.  Making decisions is something that we do every day in the real world.  For example, if a restaurant is too expensive we may want to choose a different one.  If it's too cold outside, we should find something to do inside.  These are the types of decisions we want our code to make as well.  After learning about conditionals we can do just that.  

### Learning Objectives

* Understand how an `if` statement can change the execution flow of our code when certain conditions are met
* Understand how the `if` keyword works with the `else` keyword in Python
* See how to to combine `if` statements in `for` loops

### If statement and execution flow

So far in Python, all of our lines of code have run one after the other. 


```python
vacation_days = 0
vacation_days += 1
vacation_days
```




    1



> The += is used to increment.  The statement `vacation_days += 1` can be thought of as `vacation_days = vacation_days + 1`.  So before line 2, `vacation_days` is 0.  Then we reassign `vacation_days` to equal the previous value of `vacation_days`, 0, plus one.

Contrast this with code with an `if` statement.  Once we run an `if` statement, this is no longer the case.  Code that is part of an `if` block runs does not run when the conditional argument is `False`.  


```python
vacation_days = 1
if False:
    # code does not run as conditional argument False
    vacation_days += 1
```


```python
vacation_days
```




    1



Because the code after `if` equals `False`, the code directly underneath is not run.  So, `vacation_days` stays assigned to the number 1.  

Just as we did with functions, we indicate that something is part of the block by indenting.  So we indented the line `vacation_days += 1` to ensure that whether it is run depends on the conditional argument above.  To end the block we simply stop indenting.


```python
vacation_days = 1
if False:
    # if block begins
    vacation_days += 1
# if block ends
vacation_days += 2
vacation_days
```




    3



So above, the last two lines are run as they are not part of the `if` block.

And, as you may have guessed, when the conditional argument is `True`, the code in the conditional block **does** run.  


```python
vacation_days = 1
if True:
    # code in if block runs, as True
    vacation_days += 1
vacation_days
```




    2



### Code that sometimes runs

Our code in conditional arguments becomes more interesting if we use conditional arguments that are less direct.


```python
def long_vacation(number_of_days):
    if number_of_days > 4:
        return 'that is a long vacation'
```


```python
long_vacation(5) # 'that is a long vacation'
long_vacation(3) # None
```

In the code above, you can hopefully see the power of our `if` statement.  Our `if` argument is the expression `number_of_days > 4`, which sometimes evaluates to `True` and sometimes `False`, it depends on the number of days.

Now sometimes we want to say that when something is not `True`, do something **else**.


```python
def vacation_length(number_of_days):
    if number_of_days > 4:
        return 'that is a long vacation'
    else:
        return 'not so long'
```


```python
vacation_length(3) # 'not so long'
vacation_length(5) # 'that is a long vacation'
```




    'that is a long vacation'



### Truthiness

So far our conditionals have depended on whether something exactly evaluates to `True` or `False`.  But conditionals don't force us to be so precise.  Conditionals also consider some values `True` whenever they are truthy.  Take a look at the following.


```python
vacation_days = 1
if vacation_days:
    # this is run
    vacation_days += 1
vacation_days
```




    2



However, `0` is not considered truthy.  


```python
vacation_days = 0
if vacation_days:
    # this is run
    vacation_days += 1
vacation_days
```




    0



So because of that, the `if` block is not run, `vacation_days` is not incremented, and it stays at 0. Just as if `vacation_days` equaled `False`. 

So what is truthy and what is falsy in Python?  Zero is falsy, `None` is falsy.  Also considered falsy is anything where `len` of that thing returns `False`, so `''`, `[]` are both falsy.  Let's see that. 


```python
greeting = ''
if greeting:
    greeting += 'Hello'
else:
    greeting += 'Goodbye'
greeting
```




    'Goodbye'



If we are ever curious about the whether something is truthy or falsy in Python, we can just ask with the `bool` function.


```python
bool(0) # False
bool(1) # True
```




    True



### Conditionals in Loops

Finally, we can use conditionals in loops.  This is great at filtering out certain elements and selecting just what we need.  Let's see this.


```python
greetings = ['hello', 'bonjour', 'hola', 'hallo', 'ciao', 'ola', 'namaste', 'salam']

def starts_with_h(words):
    selected = []
    for word in words:
        if word.startswith('h'):
            selected.append(word)
    return selected 

starts_with_h(greetings)
```




    ['hello', 'hola', 'hallo']



### Summary

In this lesson, we saw how conditionals allow us to make decisions with our code by only executing code under the `if` statement when the conditional argument is `True` or truthy.  We then saw how we can use the `else` statement to only run code when the conditional argument is `False` or falsy.  And as we know, code that is not in a conditional block is still run as normal.  

We examined what is truthy or falsy, and saw that None, 0, and data with a length of zero are falsy.  Finally, we saw how by using `if` in a `for` loop we can return a subset of a collection that meets a criteria.
