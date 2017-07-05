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
