# Two Bugs in My Implementation

* I used `diff` to find the tests with different results.

![Image](labrepo5-1.png)
> **Test 194**

**File content looks like this:**
![Image](labrepo5-2.png)

**My result v.s. the other result**
![Image](labrepo5-3.png)

 * I think both implementations are correct. The program should return a link which contains parentheses: my_(url).

 * My implementation is not correct. It ignores the case in which the label in brackets followed  by a colon and the link can also represent a link. 
 
 * After checking the existence of opening and closing brackets, I should check if there's any colon that imediately follows. If so, the content after the colon should be parsed as a link as well.

 ![Image](labrepo5-4.png)


> **Test 201**

**File content looks like this:**
![Image](labrepo5-5.png)

**My result v.s. the other result**
![Image](labrepo5-6.png)
