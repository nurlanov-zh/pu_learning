# pu_learning
Implementation of the paper ["Learning Classifiers from Only Positive and Unlabeled Data"](https://www.eecs.wsu.edu/~holder/courses/CptS570/fall09/present/ElkanKDD08.pdf) by Charles Elkan and Keith Noto. 

## Definitions
* *x* - input data; *y* - label is 0 or 1, *s = Indicator(x is labeled)*.
* **Scenario:** 
```markdown 
p(s = 1 | x, y = 0) = 0. (1) 
``` 
Which means only positive examples can be labeled.
* **Assumption:** 
```markdown
p(s = 1 | x, y = 1) = p(s = 1 | y = 1) = c. (2)
```
Which means that samples from positive examples have been picked, i.e. labeled, randomly with uniform distribution. 
* **Aim:** to approximate 
```markdown
p(y = 1 | x) = f(x)
```
as close as possible. 

## Approach
Given 2 subsets with "labeled" *(s = 1)* and "unlabeled" *(s = 0)* data, a standart classification algorithm can yield a function *g(x)*
```markdown
g(x) = p(s = 1 | x).
```

And under our scenario (1) and assumption (2) we get: 
```markdown
g(x) = p(s=1|x) =(1)= p(y=1 and s=1|x) = p(y=1|x)p(s=1|y=1, x) =(2)= p(y=1|x)p(s=1|y=1) = f(x)c
```
So, the main result is
```markdown
p(y=1|x) = p(s=1|x)/c
```

Where constant *c = p(s = 1| y = 1)* can be estimated on validation set *V* as follows. Let's take subset *P* of examples in *V* that are labeled, i.e. *s=1*, and hence according to (1) are positive. Then first estimator *e_1* is following:
```markdown
e_1 = 1/n sum_{x in P}(g(x)), where n = |P|,

because for any x in P:
g(x) = p(s = 1|x) = p(s = 1|x, y=1)p(y = 1|x) + p(s = 1|x, y=0)p(y=0|x) =(x in P),(1)= 
= p(s = 1|x, y=1)1 + 0 =(2)= p(s = 1| y = 1) = c
```
Second estimator *e_2*:
```markdown
e_2 = sum_{x in P}(g(x)) / sum_{x in V}(g(x))
```
Third estimator *e_3*:
```markdown
e_3 = max_{x in V}(g(x)), 
because g(x) <= c for any x
```

However, in practise and in theory the first one *e_1* has the lowest variance.
