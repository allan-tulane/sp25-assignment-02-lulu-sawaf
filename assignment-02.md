# CMPS 2200 Assignment 2

**Name:** Lulu Sawaf

In this assignment we'll work on applying the methods we've learned to analyze recurrences, and also see their behavior
in practice. As with previous
assignments, some of of your answers will go in `main.py` and `test_main.py`. You
should feel free to edit this file with your answers; for handwritten
work please scan your work and submit a PDF titled `assignment-02.pdf`
and push to your github repository.


## Part 1. Asymptotic Analysis

Derive asymptotic upper bounds of work for each recurrence below.

* $W(n)=2W(n/3)+1$

The work at the root is 1. For each level, the work of the nodes is calculated independently, the levels are split into 2 subproblems each of size n/3. Level 1 has 2 nodes that each do work 1 for a total of 2 and level 2 has (2^2=4) 4 nodes that each work on size n/3^2 for a total of 4. To extrapolate this out into number i levels, level i has 2^i nodes each doing work 1 for a total of 2^i
n/3^h = 1 therefore tree height, h, = log₃(n)
Number of nodes: 1 + 2 + 2² + ... + 2^(log₃(n)) ≈ 2^(log₃(n)+1) ≈ 2·n^(log₃(2))
Work is dominated by the leaf level because 2 > 3^0

Therefore, W(n) = Θ(n^(log₃(2))) = Θ(n^0.631)
 
* $W(n)=5W(n/4)+n$

The work at the root is n. Level 1 has 5 nodes that each do n/4 work for a total of 5n/4, therefore level i has 5^i nodes, each doing n/4^i work for a total of 5^i·(n/4^i) = n·(5/4)^i. Since (5/4) > 1, work increases with each level
n/4^h = 1 therefore height, h, = log₄(n). The final level has the most work n·(5/4)^(log₄(n)) = n·5^(log₄(n))/4^(log₄(n)) = n·5^(log₄(n))/n = 5^(log₄(n)) = n^(log₄(5))

Therefore, W(n) = Θ(n^(log₄(5))) = Θ(n^1.161)

* $W(n)=7W(n/7)+n$

The work at the root is n. Level i has 7^i nodes, each doing n/7^i work, for a total of n. The height is log₇(n) levels

Each level does same amount of work therefore the total work is n·log₇(n) = Θ(n log n)

* $W(n)=9W(n/3)+n^2$

The work at the root is n^2. Level i has 9^i nodes, each doing (n/3^i)^2 work, for a total of 9^i·(n/3^i)^2 = n^2·(9/3^2)^i = n^2·(1)^i = n^2
Height is log₃(n) levels
All levels do equal work n^2 therefore the total work is n^2·log₃(n) = Θ(n^2 log n)

* $W(n)=8W(n/2)+n^3$
* 
The work at the root is n^3. Level i has 8^i nodes, each doing (n/2^i)^2 work, for a total of 8^i·(n/2^i)^3 = n^3·(8/2^3)^i = n^3·(8/8)^i = n^3. The height is log₂(n) levels.
Each level does the same work n^3 therefore the total work is n^3·log₂(n) = Θ(n^3 log n)


* $W(n)=49W(n/25)+n^{3/2}\log n$

The work at the root is n^(3/2)·log n. Level i has 49^i nodes, each doing (n/25^i)^(3/2)·log(n/25^i) work
49^i·(n/25^i)^(3/2)·log(n/25^i) ≈ n^(3/2)·(49/25^(3/2))^i·(log n - i·log 25)
49/25^(3/2) = 49/125 < 1, so work decreases with depth

Root work dominates and therefore W(n) = Θ(n^(3/2) log n)

* $W(n)=W(n-1)+2$

 Decreases in problem size and does not branch. The work ar each level is 2, there are n total levels.
 Therefore the total work is 2n = Θ(n)

* $W(n)= W(n-1)+n^c$, with $c\geq 1$

We are solving for n-i. The work at level i is (n-i)^c and the total work is sum [(n-i)6c] for i from 0 to n-1, and it is dominated by the largest terms. The sum of k^c (from k=1 to n) is Θ(n^(c+1))
Therefore total work W(n) = Θ(n^(c+1))

* $W(n)=W(\sqrt{n})+1$

This creates a drastically shrinking problem size
Work at the root is one, at level 1   (sqrt(n)): 1, at level 2  (sqrt(sqrt(n)) = n^(1/4)): 1, at level i problem size is n^(1/2^i)
When n^(1/2^i) = 2, or 2^i = log(log n), size 2 is reached
There are log(log n) total levels and each level does work 1
Therefore total work W(n) = Θ(log log n)


## Part 2. Algorithm Comparison

Suppose that for a given task you are choosing between the following three algorithms:

  * Algorithm $\mathcal{A}$ solves problems by dividing them into
      five subproblems of half the size, recursively solving each
      subproblem, and then combining the solutions in linear time.
    
  * Algorithm $\mathcal{B}$ solves problems of size $n$ by
      recursively solving two subproblems of size $n-1$ and then
      combining the solutions in constant time.
    
  * Algorithm $\mathcal{C}$ solves problems of size $n$ by dividing
      them into nine subproblems of size $n/3$, recursively solving
      each subproblem, and then combining the solutions in $O(n^2)$
      time.

    What are the asymptotic running times of each of these algorithms?
    Which algorithm would you choose?


Algorithm A\mathcal{A} asymptotic runtime is W(n) = 5W(n/2) + n

The root work is n, at level i, 5^i nodes, each with work (n/2^i), have a total work of 5^i·(n/2^i) = n·(5/2)^i
Since 5/2 > 1, the work increases with depth. The height is log₂(n).
Work is dominated by the leaf level,
n·(5/2)^(log₂(n)) = n·5^(log₂(n))/2^(log₂(n)) = n·5^(log₂(n))/n = 5^(log₂(n)) = n^(log₂(5))

Therefore, W(n) = Θ(n^(log₂(5))) = Θ(n^2.32)


Algorithm B\mathcal{B} asymptotic runtime is W(n) = 2W(n-1) + 1

Algorithm B creates a wide tree with linear depth. The root work is 1. At level 1 there are 2 nodes, each with problem size n-1, for a total of work 2. At level 2, there are (2² = 4) 4 nodes, each with problem size n-2, work 4. At level i there are 2^i nodes, each doing work 1, for a total work of 2^i. The height is n levels. Total work is dominated by deepest level, level 2^n.

Therefore, W(n) = Θ(2^n)


Algorithm C\mathcal{C} asymptotic runtime is W(n) = 9W(n/3) + n²

The root work is ^2. At level i, there are 9^i nodes, each with work (n/3^i)^2, for a total of 9^i·(n/3^i)^2 = n^2·(9/9)^i = n^2. Each level does work n^2 and the height is log₃(n) levels total.

Therefore the total work is n^2·log₃(n) = Θ(n^2 log n)


Algorithm C\mathcal{C} is ideal.

ALgorithm A has complexity Θ(n^2.32) and therefore grows faster than C\mathcal{C} C's complexity of Θ(n² log n)
Algorithm B has an exponential complexity Θ(2^n), which is only useful for small inputs
Algorithm C has the n² log n factor and it grows slower than n^2.32 and much slower than 2^n



## Part 3: Parenthesis Matching

A common task of compilers is to ensure that parentheses are matched. That is, each open parenthesis is followed at some point by a closed parenthesis. Furthermore, a closed parenthesis can only appear if there is a corresponding open parenthesis before it. So, the following are valid:

- `( ( a ) b )`
- `a () b ( c ( d ) )`

but these are invalid:

- `( ( a )`
- `(a ) ) b (`

Below, we'll solve this problem three different ways, using iterate, scan, and divide and conquer.

**3a. iterative solution** Implement `parens_match_iterative`, a solution to this problem using the `iterate` function. **Hint**: consider using a single counter variable to keep track of whether there are more open or closed parentheses. How can you update this value while iterating from left to right through the input? What must be true of this value at each step for the parentheses to be matched? To complete this, complete the `parens_update` function and the `parens_match_iterative` function. The `parens_update` function will be called in combination with `iterate` inside `parens_match_iterative`. Test your implementation with `test_parens_match_iterative`.


.  
. 



**3b.** What are the recurrences for the Work and Span of this solution? What are their Big Oh solutions?

The iterative solution processes each element once and updates a single counter.

Work:
Each element requires constant work to process, and there are n elements
Recurrence: W(n) = n × O(1)
Big Oh: W(n) = Θ(n)

Span:
The operations are sequential (element 1 needs to be processed before element i+1)
Recurrence: S(n) = n × O(1)
Big Oh: S(n) = Θ(n)

The iterative solution has linear work and linear span and is therefore efficient in sequential processing, but not in parallel execution.



**3c. scan solution** Implement `parens_match_scan` a solution to this problem using `scan`. **Hint**: We have given you the function `paren_map` which maps `(` to `1`, `)` to `-1` and everything else to `0`. How can you pass this function to `scan` to solve the problem? You may also find the `min_f` function useful here. Implement `parens_match_scan` and test with `test_parens_match_scan`

.  
. 



**3d.** Assume that any `map`s are done in parallel, and that we use the efficient implementation of `scan` from class. What are the recurrences for the Work and Span of this solution? 

Work analysis:
Mapping each element to 1, -1, or 0, work is W_map(n) = Θ(n)
Efficient scan on n elements, work is W_scan(n) = Θ(n)
Final reduction, work is W_reduce(n) = Θ(n)

Total work is W(n) = W_map(n) + W_scan(n) + W_reduce(n) = Θ(n)

Span analysis:
Mapping in parallel, span is S_map(n) = Θ(1)
An efficient scan creates a balanced binary tree with a height of log n, span is S_scan(n) = Θ(log n)
Reduction for minimum, span is S_reduce(n) = Θ(log n)

Total span is S(n) = S_map(n) + S_scan(n) + S_reduce(n) = Θ(log n) 

**3e. divide and conquer solution** Implement `parens_match_dc_helper`, a divide and conquer solution to the problem. A key observation is that we *cannot* simply solve each subproblem using the above solutions and combine the results. E.g., consider '((()))', which would be split into '(((' and ')))', neither of which is matched. Yet, the whole input is matched. Instead, we'll have to keep track of two numbers: the number of unmatched right parentheses (R), and the number of unmatched left parentheses (L). `parens_match_dc_helper` returns a tuple (R,L). So, if the input is just '(', then `parens_match_dc_helper` returns (0,1), indicating that there is 1 unmatched left parens and 0 unmatched right parens. Analogously, if the input is just ')', then the result should be (1,0). The main difficulty is deciding how to merge the returned values for the two recursive calls. E.g., if (i,j) is the result for the left half of the list, and (k,l) is the output of the right half of the list, how can we compute the proper return value (R,L) using only i,j,k,l? Try a few example inputs to guide your solution, then test with `test_parens_match_dc_helper`.



.  
. 





**3f.** Assuming any recursive calls are done in parallel, what are the recurrences for the Work and Span of this solution? What are their Big Oh solutions?

Work:
The solution recursively divides the list into halves
The recurrence relation is W(n) = 2W(n/2) + Θ(1)
FOr the tree, the root work is Θ(1), at level i, there are 2^i nodes, each doing Θ(1) work, for a total of Θ(2^i). The height of the tree is log₂(n)

The total work is Θ(1) + Θ(2) + Θ(4) + ... + Θ(2^(log₂(n))) = Θ(2^(log₂(n)+1)) = Θ(n)

Big Oh solution: W(n) = Θ(n)

Span:
With parallel recursive calls the recurrence relation is S(n) = S(n/2) + Θ(1). Each level adds constant work and the tree has a height of log₂(n).
The total span is Θ(log n)
and the Big Oh solution is S(n) = Θ(log n)



Divide and conquer provides the same work complexity as other approaches ( that work complexity being Θ(n)), but it has a logarithmic span of (Θ(log n)), which makes it more efficient at parallel execution when compared to the linear span of the iterative approach.


