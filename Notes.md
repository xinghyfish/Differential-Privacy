# Notes on DP(Differential Privacy)

## 1 Concepts

### 1.1 Basic Concepts

#### 1.1.1 Difference

Originally, difference is a mathematical concept. In Differential Privacy, *difference* means the difference of two databases. It focuses on the data privacy of the change of the database. Naturally there are two kinds of DP: *Unbounded DP* and *Bounded DP*. Here we mainly focus on Unbounded DP.

In Unbounded DP, $D$ and $D'$ are neighbouring if $D$ can be obtained from $D'$ by adding or removing one element. Without loss of generality, we suppose that $D' = D \cup {r}$. The element $r$ is the difference of database $D$ and $D'$.



#### 1.1.2 Privacy

The meaning of *Privacy* in DP is different from that used in daily life. The two most relevant to data privacy is: **privacy as secrecy** and **privacy as control**. The two concepts are different but related. Here is the statement:

> - **privacy as secrecy**: **[Posner, 1998]** "right to conceal discreditable facts about himself" 
> - **privacy as control**: **[Westin, 1967]** "Privacy is the claim of individuals, groups, or institutions to determine for themselves when, how and to what extent information about them is communicated to others. "

The former leads to a **"prior-to-posterior"** approach, and the later leads to a **"posterior-to-posterior"** approach.



#### 1.1.3 Data Privacy

>  **Dalenius [1977]**: Access to a statistical database should not enable one to learn anything about an individual that could not be learned without access. 

It is noticeable that data privacy is different from data security. Data security refers to the protection of data that adversary cannot get illegally. However, data privacy refers to that when data is got legally, that adversary is unable to get sensitive data inversely by some mean. 



### 1.2 Advanced Concept

#### 1.2.1 Personal Data Principle (PDP)

> Data privacy means giving an individual **control** over his or her personal data. An individual's privacy **is not violated if no personal data about the individual is used**.  Privacy does not mean that no information about the individual is learned, or no harm is done to an individual; enforcing the latter is infeasible and unreasonable.



#### 1.2.2 Group Privacy/Collective Privacy

> **Bloustein [2002]**: Group privacy is an extension of individual privacy. e interest protected by group privacy is the desire and need of people to come together, to exchange information, share feelings, make plans and act in concert to attain their objectives.

In the era of big data and data publishing, the issue of group privacy is likely to become a pressing concern. 





## 2 A Primer on $\epsilon$-Differential Privacy

### 2.1 Definition of $\epsilon$-DP

#### 2.1.1 Notions

|         Sign         |                           Meaning                            |
| :------------------: | :----------------------------------------------------------: |
|    $\mathcal{A}$     |                       random algorithm                       |
| $Range(\mathcal{A})$ | the set of all possible outputs of the algorithm $\mathcal{A}$ |
|       $Pr[·]$        |                   probability of an event                    |
|         $D$          |                           database                           |



#### 2.1.2 Definition

> **Definition 2.1 $\epsilon$-Differential Privacy**.	 An algorithm $\mathcal{A}$ satisfies $\epsilon$-differential privacy ($\epsilon$-DP), where $\epsilon \geq $, if and only if for any datasets $D$ and $D'$ that *differ on one element*, we have 
> $$
> \forall\ T \subseteq Range(\mathcal{A}): Pr[\mathcal{A}(D) \in T] \leq e^{\epsilon}Pr[\mathcal{A}(D') \in T]
> $$
> where $Range(\mathcal{A})$ denotes the set of all possible outputs of the algorithm $\mathcal{A}$.

The condition above can be equivalently stated as:
$$
\forall t \in Range(\mathcal{A}): \frac{Pr[\mathcal{A}(D) \in T]}{Pr[\mathcal{A}(D') \in T]} \leq e^\epsilon
$$
where we define $\frac{0}{0}$ to be 1.

When applying DP, an important choice is the precise condition under which $D$ and $D'$ are considered to be **neighbouring**. There are two choices:

- *Unbounded DP* : $||D-D'||_1 = 1$, which means we can obtain $D$ from $D'$ by adding or deleting one element.
- *Bounded DP*: $||D -D'||_1 = 2,\ ||D||_1=||D||_2$, which means we can obtain $D$ from $D'$ by replacing one element with another one.



#### 2.1.3 Understanding the definition of DP

Since we want to protect the privacy of individual, however, we must make sure that precision of the data. $\epsilon$ is the bound of the difference. The larger $\epsilon$ is, the more different the two database will be.

In information theory, **KL-Divergence** is used to measure the difference of two random distribution. Here is the definition of **KL-Divergence**:

> **Definition 2.2 KL-Divergence/Relative Entropy**.	$Y$ and $Z$ are two random distribution, $D(Y||Z)$ is the KL-Divergence, we have
> $$
> D(Y||Z) = \mathbb{E}_{y \sim Y}[ln\frac{Pr[Y=y]}{Pr[Z=y]}]
> $$

KL-Divergence is used to measure the whole diversity of two random distribution. When $D(Y||Z)=0$, $Y$ and $Z$ is the same distribution.

Here, we don't care too much about the whole diversity of the distributions. We only need to make sure that when KL-Divergence is at the maximum, the difference can be bounded, so here we have **Max-Divergence** here:

> **Definition 2.3 Max-Divergence**	 and $Z$ are two random distribution, $D(Y||Z)$ is the KL-Divergence, we have
> $$
> D_{\infin}(Y||Z) = \max_{S \sub Supp(Y)}[ln\frac{Pr[Y=y]}{Pr[Z=y]}] = \max_{y \in Y}[ln\frac{Pr[Y=y]}{Pr[Z=y]}]
> $$

If Max-Divergence is less than $\epsilon$, we assert that the difference is bounded.





