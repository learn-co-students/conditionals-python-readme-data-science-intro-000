
# Conditionals

### Introduction

So far, we have seen how to retrieve data from our code, and manipulate that data.  What we have not learned, however, is how to make decisions with that data. Making decisions is something that we do every day in the real world. For example, if a restaurant is too expensive we may want to choose a different one. If it's too cold outside, we should find something to do inside. These are the types of decisions we want our code to make as well. After learning about conditionals we can do just that.  

### Learning Objectives

* Understand how an `if` statement can change the execution flow of our code when certain conditions are met
* Understand how the `if` keyword works with the `else` keyword in Python
* See how to select certain data by combining `if` statements in `for` loops 

### If Statement and Execution Flow

So far in Python, all of our lines of code run one after the other. So in the code below, `vacation_days` is inigially assigned to `0`, then it is reassigned by incrementing by one, and again reassigned by incrementing again by one, which brings the `vacation_days` to a total of `2`.


```python
vacation_days = 0
vacation_days += 1
vacation_days += 1
vacation_days
```




    2



> The `+=` is used to increment. The statement `vacation_days += 1` can be thought of as `vacation_days = vacation_days + 1`. On line 2, `vacation_days` is `0`. Then we reassign `vacation_days` to equal the previous value of `vacation_days`, which is `0`, plus `1`. Again we increment vacation_days on line 3, which would now equate to `1 + 1`, and finally we output the new value of `vacation_days`, `2`.


Contrast this with code that contains an `if` statement. Code that is part of an `if` block runs only when the conditional argument following the `if` evaluates to `True`. So it is not necessarily the case that every line of code runs.


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



Above we can see that since the codition following the `if` equals `False`, the code directly underneath is not run.  So, `vacation_days` stays assigned to the number 1.  

Just as we did with functions, we indicate that something is part of the block by indenting.  So the line `vacation_days += 1` is indented to ensure that whether it is run depends on the conditional argument above.  To end the block we simply stop indenting.


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



So in the above cell, the last two lines are run because they are not part of the `if` block.

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

Our code in conditional arguments becomes more interesting when we use conditional arguments that are less direct.


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

Now sometimes we want to say that when something is `True` do one thing, and when not `True` do something **else**.


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

![truthiness](truthiness.png "Truthiness")

So far our conditionals have depended on whether something evaluates exactly to `True` or `False`.  But conditionals don't force us to be so precise. Conditionals also consider some values `True` if they are `truthy` and `False` if they are `falsy`.  Take a look at the following:


```python
vacation_days = 1
if vacation_days:
    # this is run
    vacation_days += 1
vacation_days
```




    2



Even through `vacation_days` did not equal `True` above, it still ran the code in the `if` block because the value for `vacation_days` was `1`, which is considered `truthy`.

However, `0` is not considered truthy.  


```python
vacation_days = 0
if vacation_days:
    # this is not run
    vacation_days += 1
vacation_days
```




    0



Since `0` is **not** `truthy`, it is considered `falsy`. We can see that the `if` block was not run and `vacation_days` was not incremented, almost as if `vacation_days` evaluated to `False`. 

So what is truthy and what is falsy in Python?  Zero is falsy, and `None` is falsy.  Also falsy is anything where `len` of that thing returns `False`, so `''`, `[]` are both falsy.  Let's see that. 


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
```




    False




```python
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



The above `starts_with_h` function uses a `for` loop to move through the list of words one by one.  For each word, it checks if the word starts with `h` and if it does, it adds that word to the `selected` list.  Finally, the function returns that list of selected elements.  So by using the `for` loop combined with `if` we can choose elements of a list based on a specific criteria.

### Summary

In this lesson, we saw how conditionals allow us to make decisions with our code by only executing code under the `if` statement when the conditional argument is `True` or truthy.  We then saw how we can use the `else` statement to only run code when the conditional argument is `False` or falsy, and as we know, code that is not in a conditional block is still run as normal.  

We examined what is truthy or falsy, and saw that None, 0, and data with a length of zero are falsy.  If we are unsure, we can use the `bool` function to see a the boolean value of a piece of data.  Finally, we saw how by using `if` in a `for` loop we can return a subset of a collection that meets a criteria.
