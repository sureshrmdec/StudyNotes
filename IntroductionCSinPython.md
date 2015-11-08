https://courses.edx.org/courses/course-v1:MITx+6.00.1x_7+3T2015/info

## Lecture 1
Turing's Halting Problem.  

- Declarative knowledge
- Imperative knowledge  

Square root of a number: `g^2 = x` find g
- guess g
- Test: if `g^2 ~= x`, return g
- Caculation: `g = 1/2(g + x/g)`
- Flow control

A special program, interpreter, execute each instruction of a program in order.  

Computer architecture:  
- Memory
- Control unit: include a program counter
- Arithmetic logic unit: include an accumulator
- Input 
- Output

Turing complete: six primitives can compute anything.   

Static semantics: even syntax is right, sometimes not has meaning

- Compiled language
- Interpreted language

Semantic errors can not be captured by computer.  
Defensive programming can avoid semantic errors.  

## Lecture 2
Low level language: src code -> checker -> interpreter -> output  
High level language: src code -> checker -> compiler -> object code -> interpreter -> output  

Objects are: 1. scalar(cannot be subdivied) 2. non-scalar.  
Scalar objects:  
- int  
- float
- bool

`type(object)`  
`3**2`  

Type conversion: `float(3)`  

The order of boolean operations is as follows:
# Parentheses. 
# not statements.
# and statements.
# or statements.

When compare int with float, auto convert the type.  

Assignment: `=`, create a binding between variable and value.   

Non-scalar objects: compound objects.  

Operator overloading.  

`len('abc')`  

Indexing: `'abc'[0]`. `'abc'[-1]` 
Slicing: `s[start:end]`   

`'a' in 'abc'`  

`s[i:j:k]` from i to j-1 with step k. If k is negative, go backward.  

`num = float(raw_input('input a number'))`  

branching program: with flow control.  

```
if express: 
    ...
elif express:
    ...
else: 
    ....
```

Any string is always larger than integer.  

## Lecture 3
Iteration: change the test value inside the loop.  
Bisection search.  

Don't overwrite build-in functions like sum.  
https://docs.python.org/2/library/functions.html  
https://docs.python.org/release/2.3.5/ref/keywords.html  

```
x = 1
print(str(x) + "is a number")
```

Exaustive enumeration.  

`range(m, n, t)` not include n. t is the step. m, n should be same type(cannot be one int one float). If m < n, return an empty list.   

```
num = 10
for num in range(5): # num is a redefine here
    print num
````

Float:  
- binary present: x=a*2^(-1)+b*2^(-2), then x==0.ab
- x*2^p=n, then x = n/(2^p). Make n an integer(whole number), then present n in binary, and shift left the dot p times.  
- Cannot find a p to make 0.1 be a whole number. Python stop at a point by round it. 0.1 is not store as exactly 0.1 in the computer.  
- don't use x==y, instead use abs(x-y)<0.0001

`0.5%1=0.5`.   

Bisection search: work on problems with "ordering" property(value of function monotonically with input value).  
```
low = 0.0
high = x
while abs(ans**2 - x) >= epsilon: 
    if ans**2 < x: 
        low = ans
    else: 
        high = ans
    ans = (high + low) / 2
```

Print two words in a line.  
```
print "Hi",
print "there"
```

Newton-Raphson algorithm: p(x) = an*x^n + an-1*x^(n-1) + ... + a1*x + a0, find r that p(r) = 0.  
- first guess g and check
- g = g - p(g)/p'(g)  

```
if char in "aeiou": 
    print "char is a vowel. "
```

Lecture 4
Turing complete language.  

Abstruction: black box.  

docstring: inside three pair of quotes.  

In Python 2 functions can also be compared. Based on their id(object adress in memory).  

Python shell is default(global) environment.  

Function is a procedure object. Function name is an environment pointer.  
Function name is expr0, other args are expr1, 2 ...  

Function procedure has both the outer environment and itself environment that binding parameters as local variable.  

The scoping of function often called static or lexical.  

Max min value: if x<lo, return lo; if lo<x<hi, return x; if x>hi, return hi.  
Equal to return max(min(x, hi), lo)  

```
a = 10
def f(x):
      return x + a
a = 3
f(1) # 4
```
Since a is not binding as an variable, a is the global variable.  

Find root might failed if input<0 or abs(input)<1, fix is:  
```
def findRoot3(x, power, epsilon):
    if x < 0 and power%2 == 0:
        return None
    # can't find even powered root of negative number
    low = min(-1.0, x)
    high = max(1.0, x)
    ans = (high+low)/2.0
    while abs(ans**power - x) > epsilon:
        if ans**power < x:
            low = ans
        else:
            high = ans
        ans = (high+low)/2.0
    return ans
```

Import a function:  
```
# circle.py
pi = 3.14159

def area(radius):
    return pi*(radius**2)

def circumference(radius):
    return 2*pi*radius
```

Use `from` can bring the environment of the file in. A variable that has the same name won't change the value in the file.  
```
import circle
print circle.pi
from circle import *
pi = 3
print area(3)
```

Everything in python is an object.  
String is immutable, always return a new string when do actions on it.  

Lecture 5
Iteration: use a set of state variables.  

Recursion: 1. base case; 2. recursive step;   
Same as mathematical induction.  
LHS, RHS: left/right-hand side of expressions.   

A number has L at then end means it is presented in large format mode.  

Recursive to solve power, need take base case exp as 0.  

Find greatest common divisor:  
Recursive:  
```
def gcdRecur(a, b):
    '''
    a, b: positive integers
    
    returns: a positive integer, the greatest common divisor of a & b.
    '''
    if b == 0:
        return a
    return gcdRecur(b, a % b)
```

Iterative:  
```
def gcdIter(a, b):
    '''
    a, b: positive integers
    returns: a positive integer, the greatest common divisor of a & b.
    '''
    testValue = min(a, b)
    while a % testValue != 0 or b % testValue != 0:
        testValue -= 1
    return testValue
```

Hanoi Tower:  
```
def printMove(fr, to): 
    print "Move from " + str(fr) + " to " + str(to)
    
def Towers(n, from, to, spare): 
    if n == 1: 
        printMove(from, to)
    else: 
        Tower(n - 1, from, spare, to)
        Tower(1, from, to, spare)
        Tower(n - 1, spare, to, from)
```

Fibonacci numbers: several base cases.  
```
def fib(x): 
    assert type(x) == int and x >= 0 # if false, stop
    if x == 0 or x == 1: 
        return 1
    return fib(x - 1) + fib(x - 2)
```

Internal procedures.  
Divide and conquer.  

Using global variables is always a bit risky. Unless doing metering.   

Wrapper function.   

Use keyword `arguments` <b>?</b>.  

Use keyword `global` to make a variable in a function be useable in the top-level environment.  

Lecture 6
Tuple: a sequence of elements.
- `t=(1, 'two')`
- `t1+t2` create a new tuple with all elements. 
- `t[3:5]`.  
- Create a single-element tuple: `(ele,)`. Empty tuple: `t = ()`   
- Doesn't support element assignment.  

`aTup[::2]`: pick odd elements.  

List: are mutable which is different from tuple.  
- `l = [1, 'two', 3]`  
- `l = [4]`  
- `l.append(ele)`  
- list store reference rather than a copy. This is called alias. `L1 = L2` means `L1 is L2`.   
- `l = l1 + l2` concatenate two lists, is called flattening. Elements are copies.  
- When need remove elements while iterating lists, make a copy of the list: 
- If all elements in L1 is same as them in L2, `L1 == L2`. But only L2 is a reference to L1, `Li is L2`.  
- `list.pop()` return and remove the last element. `list.pop(idx)` return the element.  
- `list.extend([ele])` same to concatenate.  
- `list.index(ele)` return the index of the first ele.  

```
Lcpy = L[:]
for e in Lcpy: 
    L.remove(e)
```

Functions are first class objects.  
```
f = abs
for i in range(len(L)): 
    L[i] = f(L[i])
```

Higher order functions:  
- map: a function and a collection of arguments. `map(abs, [1, -2, 3, -4])` return a list of`[abs(1), 2, 3, 4]`. `map(min, L1, L2)`.  

Dictionary: list-like but key can be anything rather than int.   
- Key is and must be immutable. So key can be a tuple, but cannot be a list.  
- `dic = {'a':1; 'b':2}`  
- dict are unordered, and can only be access by a key.  
- `dic['newKey']=newEle`  
- `for e in dic:` actually return all the keys. Same as `dic.keys()`  
- `dic.values()`  
- `del dic['a']` `del` can release a variable.  

Interger divided is floor of the result: `-3/2 == -2`.  

`aString.lower()`.  
`aString.isalpha()`.  
`random.choice(aList)`.  

Lecture 7
Black box testing and glass box testing.  

Make the code easy to debug:  
- well design by break up codes into components.  
- Document constraints on models. What inputs and outputs are expected?  
- Try several inputs and see if the outputs are as expected.  

How to test: 
- find a collection of inputs that are likely to reveal bugs. So call test suite.  
- break al inputs into parts that are indicative. Do tests with typical cases.   
- or do random tests. So call black box testing.  
- black box testing is useful specially when implementation changed.  
- test with boundary cases.  
- glass box test is path-complete, means every potential path is tested.  
- glass box also need to test with boundary cases.  
- test all exceptions.  
- if statement: test both paths.  
- loop: not enter loop; loop execute once; loop execute more than once; all the ways to exit the loop.  
- recursive calls: no recursive; one recursive; several recursive calls.  
 
Unit testing: can catch algorithm bugs.  
Integration testing: can catch interaction bugs.  
Regression testing: tests with all old testcases.  
 
Build test drivers:  
- set up testing environmnets by code.  
- invoke codes using predefined inputs.  
- save results and report.  

Test stub:  
- simulate inputs from some parts that are not even writed.  

Kind of bugs:  
- runtime bugs: 1) overt: code crashs or running forever; covert: return a value that might be incorrect. 2) persistent; intermittent.  
- Defensive programming: test if input and throw errors before actually run the code.  
- If overt and intermittent bugs can be reproduced, then could debug them.  

How to debug:  
- do both correct testcase and incorrect testcase. Find a hypothesis.    
- keep records.  
- print statement.  
- use bisearch.  
- use simple examples to do the test.  
- after fix one bug, do not stop. there could be more bugs.  
- look for the usual supects: boundary case? wrong arguments? forgot call a function? alias bug? 
- focus on what the code is doing rather than where is the bug.  
- don't believe documentation.  

Lecture 8