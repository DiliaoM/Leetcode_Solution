### #118 Pascal's Triangle

**Problems:**

Given a non-negative integer *numRows*, generate the first *numRows* of Pascal's triangle.

![img](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)
In Pascal's triangle, each number is the sum of the two numbers directly above it.



**My Answer:** 

```python
# Using Python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        Pascal = []
        for i in range(1,numRows+1):
            a = []
            for j in range(i):
                if j==0 || j== i-1:
                    a.append(1)
                else:
                    a.append(Pascal[i-2][j-1]+Pascal[i-2][j])
            Pascal.append(a)
        return Pascal
```

```c++
// Using Cpp.
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> Pascal;
        if(numRows == 0) 
            return vector<vector<int>> {};
        
        for(int i=1;i<=numRows;i++)
        {
            vector<int> a;
            for(int j=0;j<i;j++)
            {
                if(j==0 || j==i-1)
                    a.push_back(1);
                else
                    a.push_back(Pascal[i-2][j-1]+Pascal[i-2][j]);
            }
            Pascal.push_back(a);
        }
        return Pascal;
    }
};
```



**One of best Answers:**

```python
from math import factorial as f

class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
    	R = []
    	for i in range(numRows):
    		L = []
    		for j in range(i+1):
    			L.append(round(f(i)/((f(j)*f(i-j)))))
    		R.append(L)
    	return R
		
	- Python 3
	- Junaid Mansuri
   
```

```c++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        if(numRows == 0) return vector<vector<int>> {};
        vector<vector<int>> ans{{1}};
        for(int i = 1; i < numRows; i++){
            vector<int> row{1};
            for(int j = 1; j < i; j++){
                row.push_back(ans[i-1][j-1] + ans[i-1][j]);
            }
            row.push_back(1);
            ans.push_back(row);
        }
        return ans;
    }
};
```



In the first solution, the author uses factorials which is different from most of us used. It is fast enough! And we could CONCLUDE that Learning Math is important!!!!



And the second solution, we could find that we may make some initializations. It could reduce the times of iterations.