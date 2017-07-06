https://www.hackerrank.com/domains/algorithms/implementation

--------------------------------------------------------------
## Grading
* g in [0,100]
* fail = {g: g < 40}
* if g >= 38, then if ceil5(g)-g < 3, g=ceil5(g)

```python
def solve(grades):
    # Complete this function
    for i in range(len(grades)):
        if (grades[i] >= 38) and (5 - (grades[i] % 5) < 3):
            grades[i] += 5 - (grades[i] % 5)
    return grades

n = int(input().strip())
grades = []
grades_i = 0
for grades_i in range(n):
   grades_t = int(input().strip())
   grades.append(grades_t)
result = solve(grades)
print ("\n".join(map(str, result)))
```

## Fruit House

* a: location of apple tree
* b: location of orange tree
* [s,t]: bounds of house

----a----[s________t]----b-----

N apples and M oranges fall distances da[i] and do[j] from their tree of origin.

How many apples hit house? How many oranges?

```python
def fruithouse(house, trees, apples, oranges):
    num_apples = 0
    for apple in apples:
        if house[0] <= trees[0]+apple <= house[1]: num_apples+=1
    num_oranges=0
    for orange in oranges:
        if house[0] <= trees[1]+orange <= house[1]: num_oranges+=1
    return num_apples, num_oranges

s,t = input().strip().split(' ')
s,t = [int(s),int(t)]
a,b = input().strip().split(' ')
a,b = [int(a),int(b)]
m,n = input().strip().split(' ')
m,n = [int(m),int(n)]
apple = [int(apple_temp) for apple_temp in input().strip().split(' ')]
orange = [int(orange_temp) for orange_temp in input().strip().split(' ')]
num_apples, num_oranges = fruithouse([s,t], [a,b], apple, orange)
print(num_apples)
print(num_oranges)
```

## Two Kangaroos

```python
def kangaroo(x1, v1, x2, v2):
    # Complete this function
    
    # Single Advantage:  
    #   If one kangaroo starts further ahead,
    #   but the other has a longer jump, then it's
    #   possible that they land on the same spot at
    #   the same time step.
    #
    # Double Advantage:
    #   If one kangaroo starts further ahead and 
    #   has a jump equal to or greater than the 
    #   other kangaroo, then the other kangaroo
    #   has no chance of catching up.
    #
    # Trivial Case: 
    #   Same starting position
    #
    # The Kangaroo Equations
    #   k1[n] = x1 + n*v1
    #   k2[n] = x2 + n*v2
    #
    # Assuming that v2 != v1, they shall one 
    # day meet if:
    #   x1 + n*v1 = x2 + n*v2
    #     ==>  (x2-x1) + n*(v2-v1) = 0
    #     ==>  n = (x1 - x2) / (v2 - v1)
    #
    # Pseudocode:
    #   0. if v2 == v1, then 'NO' unless x1==x2
    #   1. if n < 0: 'NO'
    #   2. if n is not an integer: 'NO'
    #   3. n >=0: 'YES'
    #
    if x1 == x2:
        return 'YES'
    else:
        if v1 == v2:
            return 'NO'
        
    n = (x1 - x2) / (v2 - v1)
    if n < 0: 
        return 'NO'
    else:
        if n != int(n):
            return 'NO'
        else:
            return 'YES'
#-------------------------------------------------    

x1, v1, x2, v2 = input().strip().split(' ')
x1, v1, x2, v2 = [int(x1), int(v1), int(x2), int(v2)]
result = kangaroo(x1, v1, x2, v2)
print(result)
```

## In Between Sets
This is my current code... It's wrongish... It over counts.
Basically, if max(A) is not in solution set, then I must determine
if g exists for max(A) < g <= min(B) s.t. g/a and b/g are integers for 
all a,b in A,B...  Also, min(B) not necessarily in solution set...
```python
def getTotalX(a, b):
    # Complete this function
    
    # For positive integer x to be "between" sets A and B of positive integers:
    #   * A is a factor of x:  x/a = int(x/a) for all a in A
    #   * x is a factor of B:  b/x = int(b/x) for all b in B
    # 
    # 1. n = min(B)/max(A) is integer 
    #   - the only element of A that can potentially meet this criterion is max(A)
    #     since it is possible that max(A)/a is integer for all a in A, but
    #     a/max(A) is not integer for a < max(A)
    #   - the only element of B that can potentially meetr this criteria is min(B)
    #     since it is possible that b/min(B) is integer for all b in B, but
    #     min(B)/b is not integer for any b > min(B)
    # 2. Necessary: n >= 1 (i.e., min(B) >= max(A))
    #   - consider that min(B) < max(A), then x always fails:
    #       (i) for any x < max(A), condition fails since x/max(A) not integer
    #      (ii) for any x > min(B), condition fails since min(B)/x not integer
    # 3. Solution: If (n >= 1) and (n is integer), then a solution exists, else no solution.
    #       * solution holds for n==1 iff () 
    #       * solution holds for all integers m 
    #         s.t. n/m is integer; the solution holds for else no solution (0); else if n==1, the
    #     
    n = min(b) / max(a)
    if (n >= 1) and (n == int(n)):
        # Solution Exists
        n = int(n)
        out_of_set = len([i+1 for i in range(1,n) if n/(i+1) == int(n/(i+1))])
        in_set =
    else:
        # No Solution Exists
        return 0 
  
```
