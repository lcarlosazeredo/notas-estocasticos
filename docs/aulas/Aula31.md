# Aula 31

**Data:** 01/06/2026

## Cadeias de Markov em Tempo Contínuo 

Consideramos $(X_t)_{t \ge 0}$ uma Cadeia de Markov dada por: 

$$X_t = Z_n \quad \text{se} \quad S_n \le t < S_{n+1}$$

Onde:

* $(Z_n)_{n \ge 0}$ é uma Cadeia de Markov em tempo discreto com matriz de transição $k = (k(x,y))_{x,y \in \mathcal{X}}$.
* $(S_n)_{n \ge 0}$ são os instantes de um ($\text{PPP}(\lambda)$) com $S_0 = 0$.
* O $\text{PPP}(\lambda)$ e a C.M. $(Z_n)_{n \ge 0}$ são independentes.


Fato: A matriz de transição $P_t = (P_t(x,y))_{x,y \in \mathcal{X}}$ onde $P_t(x,y) = \mathbb{P}(X_t = y \mid X_0 = x)$ é dada por:

$$P_t = e^{tQ}$$

Onde $Q = \lambda(k - I)$ é a **Matriz Geradora**.

---

### Observações:

#### 1. Soma das linhas de $Q$

Para todo $x \in \mathcal{X}$:

$$\sum_{y \in \mathcal{X}} Q(x,y) = 0$$

Os elementos da matriz $Q$ são definidos por:

$$Q(x,y) = \begin{cases} \lambda k(x,y), & \text{se } x \neq y \\ \lambda(k(x,x) - 1), & \text{se } x = y \end{cases}$$

#### 2. Condição Inicial

$$P_0 = e^{0Q} = I \quad \text{(Identidade)}$$

#### 3. A matriz $Q$ é a derivada de $P_t$ em $t=0$

$$P'(0) = \left. \frac{dP_t}{dt} \right|_{t=0} = \lim_{t \to 0} \frac{P_t - P_0}{t} = \lim_{t \to 0} \frac{e^{tQ} - I}{t}$$

$$\quad = \lim_{t \to 0} \frac{1}{t} \left( \sum_{k=0}^{\infty} \frac{(tQ)^k}{k!} - I \right) = \lim_{t \to 0} \left( Q + \sum_{k=2}^{\infty} \frac{t^{k-1} Q^k}{k!} \right) = Q$$

---

#### 4. Dedução dos Elementos de $Q$

**Caso $x \neq y$:**

$$P_t(x,y) = \mathbb{P}(X_t = y \mid X_0 = x)$$

$$= \mathbb{P}(X_t = y, N_t = 1 \mid X_0 = x) + \mathbb{P}(N_t \ge 2, X_t = y \mid X_0 = x)$$

$$= \mathbb{P}(Z_1 = y, N_t = 1 \mid Z_0 = x) + o(t)$$

$$= \mathbb{P}(N_t = 1)\mathbb{P}(Z_1 = y \mid Z_0 = x) + o(t)$$

$$= e^{-\lambda t} \lambda t k(x,y) + o(t)$$ 

$$\Rightarrow \lim_{t \to 0} \frac{P_t(x,y)}{t} = \lambda k(x,y) = Q(x,y)$$

**Caso $x = y$:**

$$P_t(x,x) = \mathbb{P}(N_t = 0) + \mathbb{P}(N_t = 1)\mathbb{P}(Z_1 = x \mid Z_0 = x) + o(t)$$

$$= e^{-\lambda t} + e^{-\lambda t} \lambda t k(x,x) + o(t)$$

$$= e^{-\lambda t}(1 + \lambda t k(x,x)) + o(t)$$

$$= (1 - \lambda t + o(t))(1 + \lambda t k(x,x)) + o(t)$$

$$= 1 + \lambda t k(x,x) - \lambda t + o(t)$$

$$= 1 + \lambda t (k(x,x) - 1) + o(t)$$

$$\Rightarrow \lim_{t \to 0} \frac{P_t(x,x) - 1}{t} = \lambda(k(x,x) - 1) = Q(x,x)$$

$$\Rightarrow \lim_{t \to 0} \frac{P_t - I}{t} = Q$$

---

#### 5. Parâmetro de Saída $\lambda(x)$

$$Q(x,x) = \lambda(K(x,x) - 1) = -\lambda \sum_{y \neq x} k(x,y) = -\lambda(x)$$

Onde $\lambda(x)$ representa a taxa total de saída do estado $x$:

$$\lambda(x) = \sum_{y \neq x} Q(x,y)$$

---

## Construção de uma Cadeia de Markov em Tempo Contínuo

Dada uma matriz $Q = (Q(x,y))_{x,y \in \mathcal{X}}$ **geradora** satisfazendo:

1. $Q(x,y) \ge 0, \quad \forall x \neq y$
2. $\lambda(x) = \sum_{y \neq x} Q(x,y) < \infty, \quad \forall x \in \mathcal{X}$

**Pergunta:** Como construir uma Cadeia de Markov com probabilidades de transição $P_t = (P_t(x,y))_{x,y \in \mathcal{X}}, \, t \ge 0$ que verifique:

$$\lim_{t \to 0} \frac{P_t(x,y)}{t} = Q(x,y), \quad \forall x \neq y$$

$$\lim_{t \to 0} \frac{P_t(x,x) - 1}{t} = -\lambda(x)$$

E que ademais verifiquem as **Equações de Chapman-Kolmogorov**?

Tais probabilidades de transição ficam determinadas pelas condições 1 e 2?