Imagine this array:


```python
import numpy as np
import numpy.ma as ma

np.random.seed(100)
arr = np.random.normal(loc = 20, scale = 2, size = 100)
arr_20 = arr[:20]
arr_20
```




    array([16.50046905, 20.68536081, 22.30607161, 19.49512793, 21.96264157,
           21.02843768, 20.44235934, 17.85991334, 19.62100834, 20.51000289,
           19.08394603, 20.87032698, 18.8328099 , 21.63369414, 21.34544161,
           19.79117771, 18.93743925, 22.05946537, 19.12372875, 17.76336351])



We can use Boolean arrays as masks in order to subset data.  For example, to determine whether values in the array are less than 20, you can use a Boolean array as a mask:


```python
arr_20 < 20
```




    array([ True, False, False,  True, False, False, False,  True,  True,
           False,  True, False,  True, False, False,  True,  True, False,
            True,  True])



If you have a masked array with NaN values, you can convert them to a masked array:


```python
arnan = np.array([1, 2, 3, np.nan, 5, 6, np.nan, 7, np.nan, 8, 9, 10])
print('original array with nan is:')
print(arnan)

arnan_masked = np.ma.masked_invalid(arnan)
print('masked array is:')
print(arnan_masked)
```

    original array with nan is:
    [ 1.  2.  3. nan  5.  6. nan  7. nan  8.  9. 10.]
    masked array is:
    [1.0 2.0 3.0 -- 5.0 6.0 -- 7.0 -- 8.0 9.0 10.0]


You can count how many unmasked value are present in the array as well as display the values themselves. This is a useful tool for large arrays.


```python
print("this array has", arnan_masked.count(), "unmasked values")

print("unmasked values are as follows", arnan_masked.compressed())
```

    this array has 9 unmasked values
    unmasked values are as follows [ 1.  2.  3.  5.  6.  7.  8.  9. 10.]


You can also mask values based on certain conditions.


```python
# masking values greater than 7

new_arr = arnan_masked.compressed()
new_arr_7 = np.ma.masked_greater(new_arr, 7)
print(new_arr_7)
```
