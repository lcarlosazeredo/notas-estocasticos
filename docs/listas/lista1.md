# LISTA 1

### Exercício 1
Seja $\mathcal{X}$ um conjunto finito. Considere $\mu$ e $\nu$ medidas de probabilidade em $\mathcal{X}$. Mostre que:

$$\|\mu-\nu\|_{TV} = \frac{1}{2}\sum_{x\in\mathcal{X}}|\mu(x)-\nu(x)|$$

pode ser calculada como:

$$\|\mu-\nu\|_{TV} = \max_{A\subseteq\mathcal{X}} |\mu(A)-\nu(A)|$$

onde $\mu(A) = \sum_{x\in A}\mu(x)$.

---

### Exercício 2
Seja $P = (P(x,y))_{x,y \in \mathcal{X}}$ uma matriz estocástica e $\pi$ uma medida de probabilidade em $\mathcal{X}$ tal que $\pi = \pi P$. Para cada $t \ge 0$, defina:

* $d(t) = \max_{x \in \mathcal{X}} \|P^t(x, \cdot) - \pi\|_{TV}$
* $\bar{d}(t) = \max_{x,y \in \mathcal{X}} \|P^t(x, \cdot) - P^t(y, \cdot)\|_{TV}$ 

Mostre que:  
&emsp;1. $d(t)$ é não-crescente.  
&emsp;2. $d(t) \le \bar{d}(t)$.  
&emsp;3. $\bar{d}(t) \le 2 d(t)$.  

---

### Exercício 3
Nas condições do Exercício 2, mostre que:

$$t_{mix}(\epsilon) \le t_{mix} \lceil \log_2(1/\epsilon) \rceil$$

onde $t_{mix} = t_{mix}(1/4)$ e $t_{mix}(\epsilon) = \min \{t \ge 0 : d(t) \le \epsilon\}$.  
*(use que $\bar{d}(t+s) \le \bar{d}(t) \cdot \bar{d}(s)$, i.e, $\bar{d}$ é submultiplicativa)*.

---

### Exercício 4
Considere uma Cadeia de Markov irredutível com período $d > 1$, matriz estocástica $P$ e única distribuição estacionária $\pi$. Mostre que, $\forall x, y \in \mathcal{X}$

$$\lim_{t \to \infty} \frac{P^t(x,y) + P^{t+1}(x,y) + \dots + P^{t+d-1}(x,y)}{d} = \pi(y)$$ 

---

### Exercício 5
Calcule a distribuição estacionária do **Passeio Aleatório** em $\{0, 1, \dots, 6\}$ com barreira refletora em $0$ e $6$.

---

### Exercício 6
Exercício 1.6.2 do livro da Eulália e Glauco.

**1.6.2** Uma cadeia de Markov com estados $\{1, 2, 3, 4, 5, 6\}$ tem matriz de transição:

$$P = \begin{pmatrix} 
1/4 & 0 & 0 & 0 & 3/4 & 0 \\
1/2 & 0 & 0 & 1/4 & 1/4 & 0 \\
0 & 0 & 1/3 & 0 & 0 & 2/3 \\
0 & 1/3 & 1/3 & 0 & 0 & 1/3 \\
1/2 & 0 & 0 & 0 & 1/2 & 0 \\
0 & 0 & 3/4 & 0 & 0 & 1/4
\end{pmatrix}$$

**a)** Identifique as classes de comunicação e as classifique.

**b)** A sequência $P^n$ converge? Em caso afirmativo, qual é o limite?

**c)** Qual é aproximativamente o valor de $\mathbb{P}(X_{10^5} = 1 | X_0 = 3)$, $\mathbb{P}(X_{10^4} = 1 | X_0 = 4)$ e $\mathbb{P}(X_{10^5} = 3 | X_0 = 6)$?

**d)** Qual é o número médio de visitas ao estado 2 se $X_0 = 4$?

---

### Exercício 7
Seja $P$ a matriz de transição do Passeio Aleatório no **Anel** com $m$ vértices. Suponha $m$ ímpar. Encontre o menor número de passos $t$ tal que $P^t(x, y) > 0$ para todos os estados $x$ e $y$.

---

### Exercício 8
Um grafo $G$ é **conexo** quando para dois vértices $x$ e $y$ de $G$, existe uma sequência de vértices $x_0, x_1, \dots, x_k$ tal que $x_0 = x$ e $x_k = y$ e $x_i \sim x_{i+1}$ para $0 \le i \le k-1$. Mostre que um Passeio Aleatório em um grafo finito é **irredutível** se, e somente se, $G$ é conexo.

---

### Exercício 9
Uma matriz de transição $P$ é **simétrica** se $P(x,y) = P(y,x)$ para todo $x, y \in \mathcal{X}$. Mostre que, se $P$ é simétrica, então a distribuição **uniforme** em $\mathcal{X}$ é **estacionária** para $P$.