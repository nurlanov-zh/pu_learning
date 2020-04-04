# pu_learning
Implementation of the paper ["Learning Classifiers from Only Positive and Unlabeled Data"](https://www.eecs.wsu.edu/~holder/courses/CptS570/fall09/present/ElkanKDD08.pdf) by Charles Elkan and Keith Noto. 

## Definitions
* *x* - input data; *y* - label is 0 or 1, *s = Indicator(x is labeled)*.
* **Scenario:** *p(s = 1 | x, y = 0) = 0*. Which means only positive examples can be labeled.
* **Assumption:** *p(s = 1 | x, y = 1) = p(s = 1 | y = 1) = c*. Which means that samples from positive examples have been picked, i.e. labeled, randomly with uniform distribution. 
* **Aim:** to approximate *p(y = 1 | x) = f(x)* as close as possible. 

## Approach
Given 2 subsets with "labeled *(s = 1)*" and "unlabeled *(s = 0)*" data, a standart classification algorithm can yield a function *g(x) = p(s = 1 | x)*.

And under our scenario and assumption we get: 
```markdown
g(x) = p(s=1|x) = p(y=1 and s=1|x) = p(y=1|x)p(s=1|y=1, x) = p(y=1|x)p(s=1|y=1) = f(x)c
```
