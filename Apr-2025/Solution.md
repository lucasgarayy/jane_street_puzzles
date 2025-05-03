This month's puzzle is a simple one. 
We are tasked with finding the value of $p$ such that the probability of there
existing an infinite path down and infinite complete binary tree with nodes
summing to at most 1 is exactly $1/2$.

To solve start by considering only the all zero path. Let $x$ to be the probability that there exists an infinite path of all zeros starting
from an arbitrary node. There are two possible cases:
1) This arbitrary node is 0 with probability $p$.
2) This arbitrary node is 1, no all zero path can start here so we ignore this case.

Now consider the children nodes. For an infinite all zeroes path we need:
- Current node to be 0
- At least one of its children must be the root of an infinite all zeroes path.

The probability that neither child has an infinite all zeroes path is given by:
$P(child) = (1-x)^2$ (1)
Therefore it follows that the probability that at least one child has an infinite all zeroes path for our arbitrary node is:
$1-P(child) = 1 - (1-x)^2$ (2)

Combining this equation with the prerequesite that the current node is zero gives the equation:
$x = p ·(1-(1-x)^2)$ (3)

However we are also given the possibility that there exists an infinite path with sum at most 1. Consider the same example above but the arbitrary node now has a value of 1, we have 2 cases:
1) The arbitrary node has a value of 1, so there cannot be any more 1-valued nodes in this path, given by:
    $(1-p)(1-(1-x)^2)$ (4)
    with $(1-p)$ the probability that the node value is one.
2) The arbitrary node has a value of 0, so there can be a 1-valued node in the path.
To solve this we can write a recursive function $f(p)$ in terms of $p$ such that:
$f(p) = (1-p)(1-(1-x)^2) + p(1-(1-f(p))^2)$ (5)
where the first term is the case the infinite path starts at a node with value 1 and the second term is the recursion that results from the arbitrary node being zero-valued and hence the path can have a one-valued node.
Finally, solving for $x=\frac{2p-1}{p}$ from (1) in equation (5) and setting $f(p) = 1/2$ as we are asked, we arrive at the cubic equation:
$3p^3 - 10p^2 + 12p - 4 = 0$ (6)

With an approximate solution of:
$p = 0.5306035754$ (7)

The "calculation.ipynb" contains an numerical approximation using the Newton-Raphson method.