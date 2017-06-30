
```python
def arrSum(arr):
    s=0
    for item in arr: s+=item
    return(s)

while True:
    print("Comma-separated list of numbers to sum:")
    arr = list(map(int, input(">").strip().split(',')))
    result = str(arrSum(arr))
    print(result+"\n\nWould you like to try again? (y/n)")
    result = input(">").strip().lower()[0]
    if result!='y': break

print('\nOk, dude. Peace!')
```

In this script, I like the use of the map function to turn a comma-separated
list into a python list:
```python
arr = list(map(int, input(">").strip().split(',')))
```
This does the following:
  1. input() prompts a user to input comma-sep'd list, which is recorded as a string
  2. strip() removes any whitespace from beginning or end of input string
  3. split() converts the csv into a python list of strings
  4. map() is a generator that yields int(string) for each string in list
  5. list() converts the generator to a list

I definitely like the map function, which is kind of like sapply (etc) in R.
However, if I was to create this code myself, I probably would have used a 
list comprehension:
```python
arr = [int(i) for i in input(">").strip().split(',')]
```
I'm not sure if map() is better or not --- generators are great when memory is
an issue, but its immediately converted to a list in its full entirety...
---------------------------------------------------------------------


```python
def solve(a0, a1, a2, b0, b1, b2):
    # Complete this function
    a = (a0>b0)+(a1>b1)+(a2>b2)
    b = (b0>a0)+(b1>a1)+(b2>a2)
    return a, b

a0, a1, a2 = map(int,input().strip().split(' '))
b0, b1, b2 = map(int, input().strip().split(' '))
result = solve(a0, a1, a2, b0, b1, b2)
print (" ".join(map(str, result)))
```

------------------------------------------------------------------------
Rank: 504912
------------------------------------------------------------------------
You are given an array of integers of size N. 
You need to print the sum of the elements in the array, keeping in mind that some of those integers may be quite large.

**NOTE**: Basically, for the tests they give, I could have just used sum(ar).
But I wanted to develop a more robust solution.  I *think* I did that with this
attempt at a "vector space representation" of numbers, which allows me
to do only small additions and corrections over "decadal" components.


```python
def aVeryBigSum(n, ar):
    # Complete this function
    # "Vector Space Approach" (1,2,3) = 1*10^0 + 2*10^1 + 3*10^2
    strArr = [str(i)[::-1] for i in ar]
    mxlen  = max([len(num) for num in strArr])
    vecArr = [[int(c) for c in strNum] + [0]*(mxlen-len(strNum)) for strNum in strArr]
    # list transpose
    vecArr = [[vecArr[i][j] for i in range(n)] for j in range(mxlen)]
    # sum in each component
    vecArr = [sum(i) for i in vecArr]
    # if component xyz > 9, keep first digit (z) and add xy to next component
    for i in range(n-1):
        if vecArr[i] > 9:
            vecArr[i+1] += int(str(vecArr[i])[:-1])
            vecArr[i] = int(str(vecArr[i])[-1])
    output = int(''.join(map(str,vecArr[::-1])))
    return output
    
n = int(input().strip())
ar = list(map(int, input().strip().split(' ')))
result = aVeryBigSum(n, ar)
print(result)
```

------------------------------------------------------------------------
Rank: 450703
------------------------------------------------------------------------
Given a square matrix of size NxN, calculate the absolute difference between the sums of its diagonals.
```python
def diag_diff(n, mat):
    assert len(mat) == n, 'Num(rows) must be n'
    assert len(mat[0]) == n, 'Num(cols) must be n'
    s1 = sum([mat[i][i] for i in range(n)])
    s2 = sum([mat[i][n-i-1] for i in range(n)])
    output = s1 - s2
    if output < 0:
        return -1*output
    else:
        return output

n = int(input().strip())
a = []
for a_i in range(n):
    a_t = [int(a_temp) for a_temp in input().strip().split(' ')]
    a.append(a_t)
print(diag_diff(n,a))
```

------------------------------------------------------------------------
Rank: 414583
------------------------------------------------------------------------
Given an array of integers, calculate which fraction of its elements are positive, which fraction of its elements are negative, and which fraction of its elements are zeroes, respectively. Print the decimal value of each fraction on a new line.
```python
def sgnfrac(arr):
    n = len(arr)
    d = {(True,False): 0, (False,True): 0, (False,False): 0}
    for i in arr: d[(i>0,i<0)] += 1/n
    print( '%f\n%f\n%f' %\
          (d[(True,False)],d[(False,True)],d[(False,False)]))

n = int(input().strip())
arr = [int(arr_temp) for arr_temp in input().strip().split(' ')]
sgnfrac(arr)
```

------------------------------------------------------------------------
Rank: 381340
------------------------------------------------------------------------

The Staircase Exercise 
```python
def staircase(n):
    stairs = [''.join([' ']*(n-i-1)+['#']*(i+1)) for i in range(n) ]
    for step in stairs: print(step)

n = int(input().strip())
staircase(n)
```

------------------------------------------------------------------------
Rank: 352827
------------------------------------------------------------------------
Given five positive integers, find the minimum and maximum values that can be calculated by summing exactly four of the five integers. 
Then print the respective minimum and maximum values as a single line of two space-separated long integers.
```python
# Apparently, python ints have unlimited precision
#  -- https://docs.python.org/3/library/stdtypes.html
def minmax(arr, nterms=4):
    arr.sort()
    print(sum(arr[:nterms]),sum(arr[-nterms:]))

arr = list(map(int, input().strip().split(' ')))
minmax(arr)
```

------------------------------------------------------------------------
Rank: 326668
------------------------------------------------------------------------
You suck at blowing out candles, especially when they have different heights.
In fact, we found that you can only blow out the tallest candles.


```python
def birthdayCakeCandles(n, ar):
    # Complete this function
    tallest = 0
    count = 1
    for height in ar:
        if height > tallest:
            tallest = height
            count = 1
        elif height == tallest:
            count += 1
    return count

n = int(input().strip())
ar = list(map(int, input().strip().split(' ')))
result = birthdayCakeCandles(n, ar)
print(result)

```
------------------------------------------------------------------------
Rank: 304999
------------------------------------------------------------------------

```python
def timeConversion(s):
    # Complete this function
    ss = s[0:-2]
    if s[-2:] == 'PM':
        hh = int(s[0:2])
        hh = hh + 12 if hh!=12 else hh
    else:
        hh = int(s[0:2])
        hh = 0 if hh==12 else hh
    hh = str(hh) if hh > 9 else '0'+str(hh)
    ss = hh + ss[2:]
    return ss

s = input().strip()
result = timeConversion(s)
print(result)
```
------------------------------------------------------------------------
Rank: 271932
------------------------------------------------------------------------

Left off at this challenge:

https://www.hackerrank.com/challenges/two-subarrays?h_r=next-challenge&h_v=zen
