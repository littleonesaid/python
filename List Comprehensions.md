
I have always believe that list comprehension are not a cleaner way of writing a loop the become quite complex at time as compared to normal loop but they are faster. And because they are faster I have spent a lot of time in practicing them during my early days in Python. As mentioned in <B>The Learning Python</B> By <B> Mark Lutz</B>
><i>Moreover, depending on your Python and code, list comprehensions might run much faster than manual for loop statements (often roughly twice as fast) because their iterations are performed at C language speed inside the interpreter, rather than with manual Python code. Especially for larger data sets, there is often a major performance advantage to using this expression.</i>

I recently  put this theory to test and I was greatly suprised.

### Problem: 

Calculate Square of No 1 to 100000

### Solutions


```python
def square():
    return [x**2 for x in range(100000)]
```


```python
timeit square()
```

    91.7 ms ± 4.45 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
    


```python
def square():
    new_list = []
    for x in range(100000):
        new_list.append(x**2)
    return new_list

```


```python
timeit square()
```

    92.5 ms ± 3.86 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
    

Surprise Surprise!. The speed is almost equivalend. Now lets take a slighty complex example

### Problem:

Get All Prime No from 1 to 100000

### Solution:


```python
def prime():
    return [x for x in range(1, 1000) if all([x%y for y in range(2,x)])]
```


```python
timeit prime()
```

    79 ms ± 7.75 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
    


```python
def prime():
    prime_no = []
    for x in range(1, 1000):
        result = []
        for y in range(2,x):
            result.append(x%y)
        if all(result):
            prime_no.append(x)
    return prime_no
```


```python
timeit prime()
```

    137 ms ± 11 ms per loop (mean ± std. dev. of 7 runs, 10 loops each)
    

Its slightly faster in this case. So for single `for` loop there is not much improvement in terms if speed. If go into more complex scenarios where there are nested loops converting them to list comprehension may give slight performance imporvement but generally it take toll on redability.
If you are new to python then I would recommend not to worry too much about comprehensions and jump on to more important topics. Unless you are dealing with very huge and complext data sets comprehension might not be of any use and generally for those complex scenario you may have more suitable approach like `map`, `filter` and `reduce` which are way way faster then these.

#### ***Note:***

I am no way questiong **Mark Lutz** as either the things might have been different on earlier versions of python or his data sets might be different but my observation on **Python 3.7** is list comprehensions are faster but not significantly faster then regular for loops.




```python

```
