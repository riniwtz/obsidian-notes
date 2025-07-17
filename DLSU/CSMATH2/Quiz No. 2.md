- Matrix Addition
- Scalar Multiplication
- Trace of Matrix

**Problems:**
- Determine if its a Vector Space or Not
- Getting the Trace of a Matrix
- Vector Addition and Scalar Multiplication Test
- Prove if a set is a subspace (use the 3-condition test).
- Find the span
- Find dot products, projections, angles.
- Given two vectors, find:
    - Distance
    - Angle
    - Projection
- Identify if given vectors form a vector space (based on closure rules).

**Reminders**:
- A trace of a matrix sums all diagonal entries.
- $\oplus$ and $\odot$ are only used in formal contexts and not in usual vector calculations.

---


# Real Vector Space
---
- Vector space is just a collection of objects (called **vectors**) where I can
	1. Add any two vectors and still get a vector
	2. Multiply vector by scalar, and still get a vector
	3. Follows basic rules (like zero exists, adding in any order works)

# $\mathbb{R}$ Notations
---
- $\mathbb{R}$ is a set of all real numbers ($1.2$, $0$, $\pi$, $-3$, etc.)
- Superscript $n$ describes the amount or number of coordinates in each vector
  
**Examples**
- ${\mathbb{R}^2}$ - All 2D vectors, $(x,y)$, where $x$, $y$ $\in$ $\mathbb{R}$
- $\mathbb{R}^3$ - All 3D vectors, $(x,y,z)$, where $x$, $y$, $z$ $\in$ $\mathbb{R}$
- $\mathbb{R}^n$ - $n$-dimensional real vectors, $(x_1,x_2,\dots,x_n)$


# Zero Vector
---
- Zero vectors act like zero when added, it does nothing.
- The zero vector in any $\mathbb{R}^n$ just means **"the vector of all zeros with length $n$"**.
- It also has a property called **additive identity** where it means it doesn't change when added with $\vec{v}+\vec{0}=\vec{v}$
  
**Examples**
- $\mathbb{R}^2$, the zero vector $(\vec{0})=(0,0)\in\mathbb{R}^2$
- $\mathbb{R^3}$, the zero vector $(\vec{0})=(0,0,0)\in\mathbb{R}^2$
- $\mathbb{R^n}$, the zero vector $(\vec{0})=(0,0,0,\dots,0)\in\mathbb{R}^n$

# Additive Inverse
---
- The **inverse** of $\vec{v}=(3,-2)$, then its inverse is $-\vec{v}=(-3,2)$
- In general its defined as $$\vec{v}+(-\vec{v})=\vec{0}$$ where $\vec{v}$ is a vector, $(-\vec{v})$ is the **additive inverse**, and $\vec{v}$ is the **additive identity**.

# Distributive Properties
---
- There are two distributive rules:
1. **Scalar Distribution**
	$$a(\vec{v}+\vec{v})=a\vec{u}+a\vec{v}$$
	Example
	- $2([1,2]+[3,4])=2[4,6]=[8,12]$
	
2. **Vector Distribution**
	$$(a+b)\vec{v}=a\vec{v}+b\vec{v}$$
	Example
	- $(2+3)[1,2]=5[1,2]=[5,10]$


# Real Vector Space Axioms
---
**ADDITION**
1. Commutativity of Addition
   $$\vec{u}+\vec{v}=\vec{v}+\vec{u}$$
2. Associativity of Addition
      $$(\vec{u}+\vec{v})+\vec{w}=\vec{u}+(\vec{v}+\vec{w})$$
3. Additive Identity / Zero Vector
      $$\vec{v}+\vec{0}=\vec{v}$$
4. Additive Inverse
      $$\vec{v}+(-\vec{v})=\vec{0}$$

**MULTIPLICATION**
1. Associativity of Scalar Multiplication
   $$a(b\vec{v})=(ab)\vec{v}$$
2. Identity Scalar
   $$1\cdot\vec{v}=\vec{v}$$
   
3. Distributivity of Scalar over Vector Addition
   $$a(\vec{u}+\vec{v})=a\vec{u}+a\vec{v}$$
   
4. Distributivity of Vector over Scalar Addition
   $$(a+b)\vec{v}=a\vec{v}+b\vec{v}$$


# Set Conditions In Vector Space Axioms
---
- All real numbers are valid for vectors like $(3,-2),(-1,5),(0,0)$
- But to follow the real vector space axioms, it is explicitly defined because there are custom sets such as $$W={\{(x,y)\in\mathbb{R}^2\mid x>=0\}}$$ It shows here that $x$ must be greater than or equal to $0$ and the axioms:
	


# Properties of Closure
---
- A vector or a set is both **closed** under addition and scalar multiplication.
1. Given $\vec{a}\in S$ and scalar $c$, then $c\vec{a}\in S$
2. Given $\vec{a}\in S$ and $\vec{b}\in S$, then $\vec{a}+\vec{b}\in S$

# Subspace
---
- A subspace is a subcollection of a real vector space.
- The only requirement to verify if its a subspace is when it satisfies the closure properties.

# Span
---
$$\vec{v}_1, \vec{v}_2, \dots, \vec{v}_n \in V$$ $$ a_1\vec{v}_1+a_2\vec{v}_2+\dots a_n\vec{v}_n$$
Is called a linear combination, the set of all possible combinations of these elements is called their **span**.

**Example**
$$\mathbb{R}^3\to \left(\vec{v}_1=\begin{bmatrix}2 \\ 1 \\ -1\end{bmatrix}, \ \vec{v}_2=\begin{bmatrix}0 \\ 2 \\ 2\end{bmatrix},\ \vec{v}_3=\begin{bmatrix}-1 \\ -1 \\ -1\end{bmatrix}\right)$$
$$\text{span}(\vec{v}_1, \vec{v}_2, \vec{v}_3)=a\vec{v}_1+b\vec{v}_2+c\vec{v}_3$$ where $a, b, c$ are scalars. We then distribute the scalars: $$\text{span}(\vec{v}_1, \vec{v}_2, \vec{v}_3)=\begin{bmatrix}2a \\ a \\ -1\end{bmatrix}+\begin{bmatrix}0 \\ 2b \\ 2b\end{bmatrix}+\begin{bmatrix}-c \\ -c \\ -c\end{bmatrix}=\begin{bmatrix}2a-c \\ a+2b-c \\ -a+2b-c\end{bmatrix}$$

# Variable Naming Conventions
---
- $V$ is reserved for full vector space
- $W$ is commonly used for subspaces of $V$
- $U$ is another subspace
- $M$ commonly used to represent matrix spaces
- $S$ is a subspace of $M$



# Dot Product

# Cross Product

# Geometric Interpretation

# Find the Distance between Two Vectors

# Geometic Interpretation of Dot and Cross Product

# Vector Projection from Euclidean Vector Spaces

# Getting the Line / Point of Line in the Given Vector



---
Problems


1. Find the distance between the points $P(1,3,-1,2)$ and $Q(2,1,-1,3)$
2. Verify that the Cauchy-Schwarz inequality holds for the vectors $u=(0,2,2,-1)$ and $v=(-1,1,1,-1)$.
3. Correlation
4. Let $u=(2,-1,-2)$ and $v=(2,1,3)$. Find vectors $v_1$ and $v_2$ such that $v=v_1+v_2$, where $v_1$ is parallel to $u$ and $v_2$ is perpendicular to $u$.
5. Find a vector perpendicular to both $(1,1,1)$ and $(1,-1,-2)$
6. Find the area of a triangle with vertices $(2,-5,4), (3,-4,5)$ and $(3,-6,2)$
7. Find the volume of the parallelepiped with adjacent edges $\overrightarrow{PQ}, \overrightarrow{PR}, \overrightarrow{PS},$ where the points are $P(2,0,-1), Q(4,1,0), R(3,-1,1)$ and $S(2,-2,2)$.
8. Determine vector, parametric, and cartesian equations of the line passing through the points $P(-1,2,3)$ and $Q(4,-2,4)$.
9. Find a vector equation of the line through the point $(2,0,1)$ that is parallel to the line $$\frac{x-1}{1}=\frac{y+2}{-2}=\frac{z-6}{2}$$ Does the point $(0,4,-3)$ lie on the line?
10. Find a cartesian equation of the plane with vector form $(x,y,z)=s(1,-1,0)+t(2,0,1)+(-1,1,1),$ $s,t, \in \mathbb{R}$
11. Find a vector equation for the plane containing the points $P(1,0,2), Q(1,2,3)$ and $R(4,5,6)$
12. Where does the line $$\frac{x-1}{1}=\frac{y-2}{2}=\frac{z-3}{3}$$ intersect the plane $3x+2y+z=20$?
13. Find a vector form for the line of intersection of the two planes $x+3y+2z=6$ and $3x+2y-z=11$
14. Find $W_1$ - the projection of $\vec{u}$ onto $\vec{v}$. Find $W_2$ - the vector component of $\vec{u}$ orthogonal to $\vec{v}$. Given of $U=6i-3j+9k$ and $V=4i-j+8k$

---

if "projection of $u$ onto $v$" $$\text{proj}_{\vec{v}}{\vec{u}}=\lVert u\rVert\cdot\cos{(\theta)}\cdot\hat{v}$$ which is derived to $$\text{proj}_{\vec{v}}{\vec{u}}=\lVert u\rVert\cdot\frac{\vec{u}\cdot\vec{v}}{\lVert v\rVert^2}\cdot\vec{v}$$ then what is "projection of $v$ onto $u$"?

