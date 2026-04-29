# LISTA 2

### Exercício 1
Sejam $(X_{t})_{t \ge 0}$ e $(Y_{t})_{t \ge 0}$ Cadeias de Markov independentes, tendo a mesma matriz de transição $P$.

**a)** Defina $Z_{t} = (X_{t}, Y_{t})$ para todo $t \ge 0$. Mostre que $(Z_{t})$ é uma Cadeia de Markov e determine a sua matriz de transição.

**b)** Defina $\mathcal{T}_{enc} = \min \{ t \ge 0 : X_{t} = Y_{t} \}$, o instante do primeiro encontro das cadeias $(X_{t})_{t \ge 0}$ e $(Y_{t})_{t \ge 0}$. Mostre que $\mathcal{T}_{enc}$ é um tempo de parada com respeito à cadeia $(X_{t}, Y_{t})_{t \ge 0}$.

**c)** Suponha que $\mathcal{T}_{enc}$ seja finito quase certamente. Considere a cadeia $(Z_{t})_{t \ge 0}$ definida no item a). Para cada $t \ge 0$, defina:

$$W_{t} = \begin{cases} Z_{t}, & t \le \mathcal{T}_{enc} \\ (X_{t}, X_{t}), & t > \mathcal{T}_{enc} \end{cases}$$

Mostre que $(W_{t})_{t \ge 0}$ é um acoplamento para as cadeias de Markov $(X_{t})_{t \ge 0}$ e $(Y_{t})_{t \ge 0}$.

**d)** Denote $\mathbb{P}_{x,y}$ a medida de probabilidade no espaço de probabilidade onde as cadeias $(X_{t})_{t \ge 0}$ e $(Y_{t})_{t \ge 0}$ estão definidas e sob a qual $(X_{0}, Y_{0}) = (x, y)$ com probabilidade 1. Mostre que para todo $t \ge 0$:

$$\| P^{t}(x, \cdot) - P^{t}(y, \cdot) \|_{TV} \le \mathbb{P}_{x,y}(\mathcal{T}_{enc} > t)$$

---

### Exercício 2
Considere uma cadeia de Markov $(X_{t})_{t \ge 0}$ e tempos de parada $\mathcal{T}_{1}$ e $\mathcal{T}_{2}$. Mostre que $\mathcal{T}_{1} + \mathcal{T}_{2}$, $\max \{ \mathcal{T}_{1}, \mathcal{T}_{2} \}$ e $\min \{ \mathcal{T}_{1}, \mathcal{T}_{2} \}$ são tempos de parada para $(X_{t})_{t \ge 0}$.

---

### Exercício 3
Considere uma cadeia de Markov $(X_{t})_{t \ge 0}$ e um tempo de parada $\mathcal{T}$.

**a)** Seja $A$ um evento tal que para todo $t \ge 0$, $A \cap \{ \mathcal{T} = t \}$ depende somente de $X_{0}, \dots, X_{t}$. Considere um inteiro $n \ge 1$ e defina o evento $B = A \cap \{ X_{\mathcal{T}+1} = x_{1}, \dots, X_{\mathcal{T}+n} = x_{n} \}$ para estados $x_{1}, \dots, x_{n} \in \mathcal{X}$. Mostre que, para todo $t \ge 0$, $B \cap \{ \mathcal{T} + n = t\}$ só depende de $X_{0}, \dots, X_{t}$.

**b)** Use a questão 2 e o item a) para mostrar que:

$$\mathbb{P} (X_{\mathcal{T}+1} = x_{1}, \dots, X_{\mathcal{T}+s} = x_{s} \mid A, \mathcal{T} = t, X_{\mathcal{T}} = x_{0}) = \mathbb{P}_{x_{0}} (X_{1} = x_{1}, \dots, X_{s} = x_{s})$$

para estados $x_{0}, \dots, x_{s} \in \mathcal{X}$ e evento $A$ tal que para todo $t \ge 0$, $A \cap \{ \mathcal{T} = t \}$ só depende de $X_{0}, \dots, X_{t}$.

---

### Exercício 4
Seja $(X_{t})_{t \ge 0}$ uma Cadeia de Markov com matriz P. Defina a matriz potencial (geométrica):

$$G = \sum_{t=0}^{\infty} P^{t}$$

**a)** Mostre que para $x, y \in \mathcal{X}$, $G(x,y) = \mathbb{E}_{x} [N(y)]$.

**b)** Conclua que $x$ é recorrente se, e somente se, $G(x,x) = \infty$.

**c)** Mostre que se a cadeia é irredutível e $x$ é recorrente, então $G(y,x) = \infty$ para todo $y$.

**d)** Seja $\mathcal{T}_{x}^{+,k} = \min \{ t \ge \mathcal{T}_{x}^{+,k-1} + 1 : X_{t} = x \}$ com $\mathcal{T}_{x}^{+,0} = 0$. Mostre que para todo $k \ge 1$, $\mathcal{T}_{x}^{+,k} - \mathcal{T}_{x}^{+,k-1}$ tem a mesma distribuição que $\mathcal{T}_{x}^{+,1}$.