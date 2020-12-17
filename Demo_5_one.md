### A mask can be applied to a Boolean array for various reasons. I will show 4 simple examples of how to use a mask.

1. Applying a mask to subset data using inequalities.
2. Changing a masked array with NaN values to a masked array with dashed lines. This is more aesthetically pleasing when visualizing an array.
3. Counting unmasked values in the array. This is especially helpful for large arrays.
4. Applying a mask value to certain conditions. This is similar to the first example, but is useful for subsetting data based on a defined condition.


```python
import numpy as np
import numpy.ma as ma
```

Example 1: Applying a mask to subset data using inequalities


```python
#create an array 'arr' of 20 values

np.random.seed(100)
arr = np.random.normal(loc = 20, scale = 2, size = 100)
arr_20 = arr[:20]
arr_20
```




    array([16.50046905, 20.68536081, 22.30607161, 19.49512793, 21.96264157,
           21.02843768, 20.44235934, 17.85991334, 19.62100834, 20.51000289,
           19.08394603, 20.87032698, 18.8328099 , 21.63369414, 21.34544161,
           19.79117771, 18.93743925, 22.05946537, 19.12372875, 17.76336351])




```python
#determine whether values in an array are less than 20

arr_20 < 20
```




    array([ True, False, False,  True, False, False, False,  True,  True,
           False,  True, False,  True, False, False,  True,  True, False,
            True,  True])



Example 2: Changing a masked array with NaN values to a masked array with dashed lines


```python
#create a masked array with NaN values

arnan = np.array([1,2,3,np.nan, 5,6,np.nan, 7, np.nan, 8, 9, 10])
print('original array with nan is:')
print(arnan)
```

    original array with nan is:
    [ 1.  2.  3. nan  5.  6. nan  7. nan  8.  9. 10.]



```python
#masking this array using '--'

arnan_masked = np.ma.masked_invalid(arnan)
print('masked array is:')
print(arnan_masked)
```

    masked array is:
    [1.0 2.0 3.0 -- 5.0 6.0 -- 7.0 -- 8.0 9.0 10.0]


Example 3: Counting unmasked values in the array


```python
print('this array has', arnan_masked.count(), 'unmasked values')

print('unmasked values are as follows', arnan_masked.compressed())
```

    this array has 9 unmasked values
    unmasked values are as follows [ 1.  2.  3.  5.  6.  7.  8.  9. 10.]


Example 4: Appplying a mask value based on a condition


```python
#creating a new array called new_arr

new_arr = arnan_masked.compressed()

#the condition is to mask values greater than 7 using '--'

new_arr7 = np.ma.masked_greater(new_arr, 7)
print(new_arr7)
```

    [1.0 2.0 3.0 5.0 6.0 7.0 -- -- --]

