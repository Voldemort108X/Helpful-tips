# Multiprocessing
1. iterative process function(var) from var_list and return a list of the function output
```
list(map(lambda variable: function(variable), variable_list))
```
2. filter: condition (e.g. if) multiprocess
```
list(filter(lambda variable: condition(variable), variable_list))
```
# Numpy
1. Be aware of the row (axis=1) and column (axis=0) sum for matrices when calculating norms etc.

# Value swap or object swap
Be careful when assigning a value for arrays. For instance, if we are doing something like
```
c = a
def swap(int a, int b):
  temp = b
  b = a
  a = temp
  return a, b
swap(a, b)
```
The value of c will remain unchanged. However, if we are doing something like
```
c = a
def swap(np.array(a), np.array(b)):
  temp = b
  b = a
  a = temp
  return a, b
swap(a, b)
```
The value of c will be changed to b. Thus, try to use np.copy() without corrupting the source value.
