## April 2025 Puzzle

This month's puzzle is a simple one.

We are tasked with finding the value of \( p \) such that the probability of there existing an infinite path down an infinite complete binary tree with node values summing to at most 1 is exactly \( \frac{1}{2} \).

---

### Step 1: The All-Zero Path

Start by considering only the all-zero path. Let \( x \) be the probability that there exists an infinite path of all zeros starting from an arbitrary node.

There are two possible cases:
1. The arbitrary node has value 0 (probability \( p \)),
2. The node has value 1 — in which case no all-zero path can start here.

Now consider the children. For an infinite all-zero path to exist, we need:
- The current node to be 0,
- At least one of its children to be the root of an infinite all-zero path.

The probability that **neither** child continues an all-zero path is:

<div align="center">  
(1)  
$P_{\text{fail}} = (1 - x)^2$
</div>

Thus, the probability that **at least one child** continues the path is:

<div align="center">  
(2)  
$$
1 - (1 - x)^2
$$
</div>

Combining this with the requirement that the current node is 0, we get:

<div align="center">  
(3)  
$$
x = p \cdot \left(1 - (1 - x)^2\right)
$$
</div>

---

### Step 2: Allowing One Node With Value 1

We now expand the model to allow one node in the path to have value 1 (total sum at most 1).

We define \( f(p) \) to be the probability that there exists an infinite path with at most one node of value 1. Consider two cases:

#### Case 1: The root has value 1

Then no further 1s are allowed. The remaining path must be all zeros. This occurs with probability:

<div align="center">  
(4)  
$$
(1 - p) \cdot \left(1 - (1 - x)^2\right)
$$
</div>

#### Case 2: The root has value 0

Then a future node may be 1, and the rest must be zeros. Recursively, this occurs with probability:

<div align="center">  
(5)  
$$
p \cdot \left(1 - (1 - f(p))^2\right)
$$
</div>

Hence, we obtain the recursion:

<div align="center">  
(6)  
$$
f(p) = (1 - p) \cdot \left(1 - (1 - x)^2\right) + p \cdot \left(1 - (1 - f(p))^2\right)
$$
</div>

From equation (3), solving for \( x \), we get:

<div align="center">  
(7)  
$$
x = \frac{2p - 1}{p}
$$
</div>

Substituting equation (7) into equation (6) and solving for the condition \( f(p) = \frac{1}{2} \), we arrive at the cubic:

<div align="center">  
(8)  
$$
3p^3 - 10p^2 + 12p - 4 = 0
$$
</div>

---

### Final Answer

Solving this cubic numerically (see `calculation.ipynb`), we find:

<div align="center">  
(9)  
$$
p \approx 0.5306035754
$$
</div>

This is the critical value for which the probability of an infinite path with node sum at most 1 equals \( \frac{1}{2} \).

