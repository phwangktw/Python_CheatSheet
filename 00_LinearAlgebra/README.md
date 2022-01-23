# Python_CheatSheet_for Linear Algebra


## Load data
### Read csv
* read csv as numpy array:

```python
np.genfromtxt("position.csv", delimiter=',', skip_header = 0)
```


### Matrix Operation
* Baisc operation
    <details>
    <summary> `np.concatenate` </summary>

    ```python
        a = np.array([[1, 2], [3, 4]])
        b = np.array([[5, 6]])

        np.concatenate((a, b), axis=0)
        array([[1, 2],
            [3, 4],
            [5, 6]])
        
        np.concatenate((a, b.T), axis=1)
        array([[1, 2, 5],
            [3, 4, 6]])

        np.concatenate((a, b), axis=None)
        array([1, 2, 3, 4, 5, 6])
    ```

    </details>

    <details>
    <summary> `np.reshape` </summary>

    ```python
        a_ = a.reshape(-1,1)

        a = (250,)
        a_ = (250,1)
    ```

    </details>

    <details>
    <summary> `np.dot` and `np.matmul` (內積)</summary>

    ```python
    In [17]: a = np.array([i for i in range(6)]).reshape([3,2])

    In [18]: a
    Out[18]: 
    array([[0, 1],
        [2, 3],
        [4, 5]])

    In [19]: b=np.array([[0],[1]])

    In [20]: b
    Out[20]: 
    array([[0],
        [1]])

    In [21]: a*b
    ---------------------------------------------------------------------------
    ValueError: operands could not be broadcast together with shapes (3,2) (2,1)

    In [22]: np.multiply(a,b)
    ---------------------------------------------------------------------------
    ValueError: operands could not be broadcast together with shapes (3,2) (2,1)

    In [23]: np.matmul(a,b)
    Out[23]: 
    array([[1],
        [3],
        [5]])

    In [24]: np.dot(a,b)
    Out[24]: 
    array([[1],
        [3],
        [5]])
    -----------------------------------
    ```

    </details>

    <details>
    <summary> `np.multiply` (對應位子相乘)</summary>

    ```python
        (empty)
    ```

    </details>

    <details>
    <summary> `np.inv` (反矩陣)</summary>

    ```python
        ainv = inv(a)
    ```

    </details>