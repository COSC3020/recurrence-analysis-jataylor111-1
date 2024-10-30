# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

--------------------------------------------------------------------------------------------------

There are 3 recursive calls with n/3, and 3 for loops, two with $n^2$ complexity and one with $n$, this builds an initial equation of; $3T(\frac{n}{3}) + n^5$ but since it terminates when $n \leq 1$ we get the relation; 

$$
T(n) = \begin{cases} 
1, & \text{if } n \leq 1 \\
3T(\frac{n}{3}) + n^5, & \text{if } n > 1 
\end{cases}
$$

to find the recurrance complexity we need to subsitute a few times.

$3[3T(\frac{n}{9}) + (\frac{n}{3})^5] + n^5$ = $9T(\frac{n}{9}) + 3(\frac{n}{3})^5 + n^5$

$9[3T(\frac{n}{27}) + (\frac{n}{9})^5] + 3(\frac{n}{3})^5 + n^5$ = $27T(\frac{n}{27}) + 9(\frac{n}{9})^5 + 3(\frac{n}{3})^5 + n^5$

After simplifying;

$27T(\frac{n}{27}) + n^5 + \frac{n^5}{9^4} + \frac{n^5}{3^4}$

which becomes;

$27T(\frac{n}{27}) + n^5 + \frac{n^5}{3^8} + \frac{n^5}{3^4}$

$3^iT(\frac{n}{3^i}) + n^5\Sigma_{i=0}^{log_3{n}} \frac{1}{3^{4i}}$

This summation is a geometric series of $(\frac{1}{3})^{4i}$ where $\frac{1}{3} = r$, so;

$\Sigma_{i=0}^{log_3{n}} r^{4i} = \frac{1}{1-r}$  = $C$ 

$3^iT(\frac{n}{3^i}) +n^5C$

which since C is just a constant we can ignore it going forward and we have

$3^iT(\frac{n}{3^i}) +n^5$

let $i = log_3{n}$

$3^{log_3{n}}T(\frac{n}{3^{log_3{n}}}) + n^5 = nT(\frac{n}{n}) + n^5 = nT(1) + n^5$

which since the $nT(1)$ is of lower order to $n^5$ we get a final complexity of $O(n^5)$


I had to hunt down the markdown code for the relation at the top, from this link in the code view starting at line 682 (https://github.com/Experience-Monks/math-as-code/blob/master/README.md?plain=1#piecewise-function)

I had gotten stuck in the sigma portion and had to get help from Ali who pointed out the geometric series

I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice










