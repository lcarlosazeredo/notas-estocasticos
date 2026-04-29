# Aula 19: 

**Data:** 29/04/2026

## Cadeia Reversa
Seja $(X_t)_{t \ge 0}$ C.M. com matriz de transição $P$ irredutível e espaço de estados $\mathcal{X}$ finito. Existe uma distribuição estacionária $\pi$, com $\pi(x) > 0, \forall x \in \mathcal{X}$.

Defina a matriz de transição da cadeia reversa $\hat{P}$ como:

$$\hat{P}(x,y) = \frac{\pi(y) P(y,x)}{\pi(x)}, \quad x,y \in \mathcal{X}$$

E note que $\hat{P} = (\hat{P}(x,y))_{x,y}$ é uma matriz estocástica, pois para todo $x \in \mathcal{X}$:

$$\sum_{y \in \mathcal{X}} \hat{P}(x,y) = \frac{1}{\pi(x)} \sum_{y \in \mathcal{X}} \pi(y) P(y,x) = \frac{1}{\pi(x)} \cdot \pi(x) = 1$$

Além disso, observe que:

1. **$\pi$ é distribuição estacionária para $\hat{P}$**:
   $\pi \hat{P}(y) = \sum_{x \in \mathcal{X}} \pi(x) \hat{P}(x,y) = \sum_{x} \pi(y) P(y,x) = \pi(y), \quad \forall y \in \mathcal{X}$

2. $\pi(x) \hat{P}(x,y) = \pi(y) P(y,x), \quad \forall x,y \in \mathcal{X}$

3. $\mathbb{P}_\pi (X_t = y \mid X_{t+1} = x) = \hat{P}(x,y)$

> **Definição:** A **Cadeia Reversa** é a Cadeia de Markov cuja matriz de transição é $\hat{P}$. A cadeia $(X_t)_{t \ge 0}$ é **Reversível** se, e somente se, $P = \hat{P}$.

---

## Método de Monte Carlo Via Cadeia de Markov (MCMC)

**Problema:**
Dado um espaço $\mathcal{X}$ finito e $\pi$ uma medida de probabilidade em $\mathcal{X}$. Fixada uma função $f: \mathcal{X} \to \mathbb{R}$, queremos estimar:

$$\mathbb{E}_\pi[f] = \sum_{x \in \mathcal{X}} f(x) \pi(x)$$

onde $\pi(x)$ é conhecida apenas parcialmente.

**Solução via o Método de Metropolis-Hastings:**
Construir uma matriz estocástica $P$ tal que $\pi = \pi P$ e gerar amostras de uma Cadeia de Markov tendo $P$ como matriz de transição, a partir de diferentes condições iniciais dada uma amostra $X_0, X_1, \dots, X_T$, o **Teorema Ergódico** nos diz que:

$$\frac{1}{T+1} \sum_{t=0}^{T} f(X_t) \approx \mathbb{E}_\pi[f]$$

---

Considere $Q = (Q(x,y))_{x,y \in \mathcal{X}}$ uma matriz estocástica e uma família $\alpha = (\alpha(x,y))_{x,y \in \mathcal{X}}$ de probabilidade e defina:

$$P(x,y) = \alpha(x,y) Q(x,y), \text{ se } y \neq x \quad e$$

$$P(x,x) = Q(x,x) + \sum_{y \neq x} (1 - \alpha(x,y)) Q(x,y)$$

**Note:**

1. $P(x,y) \geq 0, \forall x,y \in \mathcal{X}$

2. $\sum_{y \in \mathcal{X}} P(x,y) = P(x,x) + \sum_{y \neq x} P(x,y)$
   $= P(x,x) + \sum_{y \neq x} \alpha(x,y) Q(x,y)$
   $= Q(x,x) + \sum_{y \neq x} (1 - \alpha(x,y)) Q(x,y) + \sum_{y \neq x} \alpha(x,y) Q(x,y)$
   $= Q(x,x) + \sum_{y \neq x} Q(x,y) = 1$

---

A dinâmica de uma C.M. com a matriz de transição $P$ pode ser descrita da seguinte forma:

Em cada passo, escolha um estado $y$ para visitar com a matriz $Q$.

Se $y$ difere do estado atual $x$, aceite a transição com prob. $\alpha(x,y)$, independentemente das demais transições. Quando uma transição não é aceita, a cadeia permanece no estado atual $x$.

Vamos escolher $\alpha$ de modo que:

$$\pi(x) P(x,y) = \pi(y) P(y,x), \quad \text{para } x \neq y$$

$$\iff \pi(x) \alpha(x,y) Q(x,y) = \pi(y) \alpha(y,x) Q(y,x), \quad x \neq y$$

Uma escolha possível é:

$$\alpha(x,y) = \min \left\{ 1, \frac{\pi(y) Q(y,x)}{\pi(x) Q(x,y)} \right\}, \quad x \neq y$$

---


De fato, se $\alpha(x,y) < 1$ então $\alpha(y,x) = 1$.

Logo,

$$\pi(x) \alpha(x,y) Q(x,y)$$

$$= \pi(x) \left( \frac{\pi(y) Q(y,x)}{\pi(x) Q(x,y)} \right) Q(x,y)$$

$$= \pi(y) Q(y,x) \alpha(y,x)$$

Com essa escolha temos que $\pi$ é distribuição estacionária para $P$.

---

### **AF.1** 
Se $Q$ é irredutível e

$$Q(x,y) > 0 \overset{(\star)}{\iff} Q(y,x) > 0,$$

então $P$ é irredutível.

#### **Prova:** 
Fixe $x$ e $y$. Como $Q$ é irredutível, então existem estados $x = x_0, x_1, \dots, x_t = y$ tais que:

$$Q(x_0, x_1) Q(x_1, x_2) \dots Q(x_{t-1}, x_t) > 0.$$

A condição $(\star)$ garante que $\alpha(x_i, x_{i+1}) > 0$, para $i = 0, \dots, t-1$.

Logo,

$$\prod_{i=0}^{t-1} \underbrace{\alpha(x_i, x_{i+1}) Q(x_i, x_{i+1})}_{P(x_i, x_{i+1})} > 0$$

$\Rightarrow P$ é **irredutível**.

---

### **AF.2** 
$P$ é aperiódica se $Q(x,x) > 0$ para algum $x$ ou $\min \{ \alpha(x,y), \alpha(y,x) \} < 1$ para algum $x \neq y$.

#### **Prova:** (Exercício)

---

## **Exemplo:** 
$G = (V, E)$ finito.

$V$ e $E$ são desconhecidos. Entretanto, suponha que seja possível realizar um P.A. simples em $G$. Se o grafo não é regular, então a distribuição estacionária do passeio não é a dist. uniforme em $V$.

Como modificar o P.A. de modo que a sua dist. estacionária seja uniforme em $V$?

Neste caso, $\pi(x) = \frac{1}{|V|}$ e

$$Q(x,y) = \begin{cases} \frac{1}{g(x)} & \text{se } y \sim x \\ 0 & \text{c.c.} \end{cases}$$

De modo que

$$\alpha(x,y) = \min \left\{ 1, \frac{\pi(y) Q(y,x)}{\pi(x) Q(x,y)} \right\}$$

$$= \min \left\{ 1, \frac{g(x)}{g(y)} \right\}, \text{ se } x \sim y$$


E podemos definir $\alpha(x,y)$ de maneira arbitrária para $x \nsim y$.

---

