## Introduction
- what is computing?
  - data: representation of objects
  - algorithms: operations on data
- core questions in computing:
  - what can and can't you actually compute?
  - can computers solve a question P?
    - what does it mean to solve it?
- in this class, the order of importance is definition > theorems > proofs

### Representing Data as Binary Strings
- all forms of data (integers, audio, images, etc) can be encoded into just binary strings
  - note that we can compose representations, i.e. if we can represent objects of type T, then we can represent collections of objects of type T
- **Definition** $$E:\Theta \to \{0,1\}^*$$ is an encoding function if and only if there exists a mapping $$D:\binstr \to \Theta$$ such that for all $x\in \Theta$, $D(E(x))=x$.
  - note that $E$ *has* to be an one-to-one mapping, i.e. $$x\neq y \implies E(x)\neq E(y)$$
  - Kleene star notation means that $\{0,1\}^*$ is a sequence of 0s and 1s
- example:
  - unary representation of natural numbers $\N = \{0,1,2,\dots\}$
    - $E(0) = 0, E(1) = 00, E(2) = 000,\dots$
  - binary represention of $\N$
    - $E(0) = 0, E(1) = 1, E(2) = 01, E(3) = 11,\dots$
    - define $NtoB:\N \to \binstr$
- **Definition**
  - $E:\theta \to \binstr$ is **prefix free** if $\forall x,y\in \Theta$ $$x\neq y \implies E(x)\text{ not a prefix of } E(y)$$
- **Theorem**
  - Suppose we have a prefix free encoding $pE: \theta\to\binstr$. Then $$\overline{pE}: \Theta^* \to \binstr$$ defined by $$\overline{pE} ([x_0,x_1,\dots,x_k]) = pE(x_0)\circ pE(x_1)\circ\dots\circ pE(x_k)$$ is an encoding.
  - Remark: Given a prefix free encoding $pE$, $\overline{pE}$ is not necessarily prefix free.
- **Claim**
  - Given any encoding $E$, we can build a prefix free encoding $pE$ from it.
    - Algorithm:
      - compute $E(x)$
      - duplicate each bit
      - append $01$
    - eg $E(5)=101\implies pE(5)=11001101$
    - Efficiency: $pE = 2E+2$
- Note: we can assume in any algorithm that the input is a binary string
- Cantor in 1876: there is no one-to-one mapping from $\R\to\binstr$

## Algorithms
- informally, an algorithm is a series of steps to solve some problem
  - problem - transform the input into some desired output
    - **specification** - function $f:\binstr\to\binstr$
  - series of steps - some basic operations

### Boolean Circuits
- simple operations
  - $AND:\zeroone\times\zeroone\to\zeroone$
    - $AND(a,b)$
      - $=1\text{ if }a=b=1$
      - $0\text{ else}$
  - $OR:\zeroone\times\zeroone\to\zeroone$
    - $OR(a,b)$
        - $=0\text{ if }a=b=0$
        - $1\text{ else}$
  - $NOT: \zeroone\to\zeroone$
    - $NOT(a,b)$
    - $=1\text{ if }a=0$
    - $=0\text{ if }a=1$