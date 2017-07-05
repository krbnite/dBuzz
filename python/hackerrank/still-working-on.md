

## Two Subarrays

https://www.hackerrank.com/challenges/two-subarrays/problem

### Consider an array of n integers, A = a[0], a[1], ..., a[n-1].
* Subsequence: an derived from dropping 0-n elements of sequence A
* Strictly-Increasing Subsequence (SIS): b[i] > b[j] for all i > j and b[i],b[j] in A
* Subarray: a contiguous subsequence of A

### Some functions on the array
* sum(l,r) = sum{ a[i] for l <= i <= r }
* inc(l,r) = maxsum{ SIS in A[l:r] }
* f(l,r) = sum(l,r) - inc(l,r)
* g = max{f(A; l,r): for 0 <= l <= r <= n}

So f measures how monotonic-increasing A is on a given subarray, A[l:r].  
If A[l:r] is a SIS itself, then f will give zero.  If A[l:r] is a strictly
decreasing subsequence, then f would give sum(l,r).  

So...it seems g is measuring how non-SIS an array is... Specifically, if g == sum(0,n-1),
then A is a non-increasing sequence, whereas if g == 0, then A is strictly increasing.  
For 0 < g < sum(0,n-1), we have non-monotonicity of some sort.

### Problem
* Let m be the length of the smallest subarray s.t. f(l,r)=g.  
* Given A, find g, m, and the number of subarrays where g and m hold true
* Constraints
  - 1 <= n <= 2*10^5
  - -40 <= a[i] <= 40
  
  
def asum(arr,l,r):
   n = len(arr)
   assert l >= 0,'Indices are positive semidefinite.'
   assert r <= n-1,'Indices must be range of array.'
   return sum(arr[l:r+1])
