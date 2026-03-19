# Aula 04

**Data:** 16/03/2026

## 1. Revisão: Cadeia de Markov com 2 Estados

$(X_t)_{t \ge 0}$ C.M. com espaço de estados $\mathcal{X} = \{0, 1\}$

Matriz de transição $P = \begin{pmatrix} P(0,0) & P(0,1) \\ P(1,0) & P(1,1) \end{pmatrix} = \begin{pmatrix} 1-p & p \\ q & 1-q \end{pmatrix}$
$\quad p, q \in [0, 1]$

$\pi = (\pi(0), \pi(1)) = \left( \frac{q}{p+q}, \frac{p}{p+q} \right)$, para $p, q \ge 0$

$\pi$ é uma **distribuição estacionária**  
$\pi = \pi P \iff \pi(y) = \sum_{x \in \mathcal{X}} \pi(x) P(x,y), \quad y \in \mathcal{X}$

---

Para $t \ge 0$, defina:
$\begin{cases} \mu_t = (\mu_t(0), \mu_t(1)) = (\mathbb{P}(X_t=0), \mathbb{P}(X_t=1)) \\ \Delta_t = \mu_t(0) - \pi(0) \end{cases}$
> $\hookrightarrow$ $\mu_t$ é o vetor de prob. da C.M. no tempo $t$.

Mostramos que:
$\Delta_t = (1-p-q) \Delta_{t-1}$

Iterando, temos:
$\Delta_t = (1-p-q)^t \Delta_0$

---

Observações:

1. Se $\Delta_0 = 0 (\implies \mu_0 = \pi)$, então $\Delta_t = 0, \forall t \ge 0 (\implies \mu_t = \pi)$

2. $|\mu_t(1) - \pi(1)| = |(1 - \mu_t(0)) - (1 - \pi(0))| = |\pi(0) - \mu_t(0)| = |\mu_t(0) - \pi(0)| = |1-p-q|^t \cdot |\Delta_0|$

3. As observações 1 e 2 nos permitem mostrar que:
   $d_{VT}(\mu_t, \pi) = \frac{1}{2} \left[ |\mu_t(0) - \pi(0)| + |\mu_t(1) - \pi(1)| \right] = |1-p-q|^t \cdot |\Delta_0|$
   > $\hookrightarrow$ (Distância de Variação Total entre $\mu_t$ e $\pi$)

4. $|\Delta_0| = |\mu_0(0) - \pi(0)| \le 1$ para qualquer escolha de $\mu_0$.

Logo, $d_{VT}(\mu_t, \pi) \le |1-p-q|^t$
> $\hookrightarrow$ converge exponencialmente rápido.

---

## 2. Generalização para Espaços Finitos

Considere C.M. $(X_t)_{t \ge 0}$ com $\mathcal{X}$ **finito** e matriz de transição $P = (P(x,y))_{x,y \in \mathcal{X}}$

$Def.:$ $\pi = (\pi(x))_{x \in \mathcal{X}}$ t.q. $\pi(x) \ge 0$ e $\sum_{x \in \mathcal{X}} \pi(x) = 1$ é uma **distribuição estacionária** se $\pi = \pi P \iff \pi(y) = \sum_{x \in \mathcal{X}} \pi(x) P(x,y)$

---

**Prop. 1:**
Se $X_0 \sim \pi$ e $\pi$ é dist. estacionária, então $X_t \sim \pi$ para todo $t \ge 0$.

**Prova:**
Note que $\forall y \in \mathcal{X}, \forall t \ge 1$:

$$
\begin{aligned}
\mathbb{P}(X_t = y) &= \sum_{x \in \mathcal{X}} \mathbb{P}(X_{t-1}=x, X_t=y) \\
&= \sum_{x \in \mathcal{X}} \mathbb{P}(X_{t-1}=x) \mathbb{P}(X_t=y \mid X_{t-1}=x) \\
&= \sum_{x \in \mathcal{X}} \mathbb{P}(X_{t-1}=x) P(x,y)
\end{aligned}
$$

Denotando, $\mu_t = (\mu_t(x))_{x \in \mathcal{X}}$  
onde $\mu_t(y) = \sum_{x \in \mathcal{X}} \mu_{t-1}(x) P(x,y)$.

Isto é,   
$\qquad \mu_t = \mu_{t-1} P$

---

Iterando, $\forall t \ge 1$:

$$
\begin{aligned}
\mu_t &= \mu_{t-1} P \\
&= (\mu_{t-2} P) P \\
&\vdots \\
&= \mu_0 P^t
\end{aligned}
$$

Agora, como $\mu_0 = \pi$ e $\pi$ é estacionário, temos

$$\pi = \pi P \Rightarrow \pi P^2 = (\pi P) P = \pi P = \pi$$

$$\Rightarrow \pi P^3 = (\pi P) P^2 = \pi P^2 = \pi$$

$$
\begin{aligned}
\Rightarrow \mu_t &= \mu_0 P^t \\
&= \pi P^t \\
&= (\pi P) P^{t-1} \\
&= \pi P^{t-1} \\
& \vdots \\
&= \pi
\end{aligned}
$$


---

## 3. Processos Estacionários

**Notação e Definições**

Quando for importante enfatizar que a dist. inicial é dada pelo vetor de probs $\mu = (\mu(x))_{x \in \mathcal{X}}$ escreveremos $\mathbb{P}_\mu$. Em particular, $\mathbb{P}_\mu(X_0 = x) = \mu(x)$.

A medida de prob. $\delta_x = (\delta_x(y))_{y \in \mathcal{X}}$  

$$\delta_x(y) = \begin{cases} 1 & \text{se } y=x \\ 0 & \text{c.c.} \end{cases}$$  

Quando $\mu = \delta_x$, escrevemos $\mathbb{P}_x$ ao invés de $\mathbb{P}_{\delta_x}$.

$Def.:$ Dado um processo Estocástico indexado por $\mathbb{N}$, i.e., uma seq. $(X_t)_{t \ge 0}$, é dito **estacionário** se: 

$$\mathbb{P}(X_0 = x_0, X_1 = x_1, \dots, X_t = x_t) = \mathbb{P}(X_s = x_0, X_{s+1} = x_1, \dots, X_{s+t} = x_t)$$  

$\forall s, t \ge 0$ e $\forall x_0, \dots, x_t \in \mathcal{X}$.

> Não confundir vetor estacionário $\pi$ com processo estacionário!


**Exemplos:**  
* Se $t=0$: $\mathbb{P}(X_0 = x_0) = \mathbb{P}(X_s = x_0), \forall s \ge 0, \forall x_0 \in \mathcal{X}$.  
* Se $t=1$: $\mathbb{P}(X_0 = x_0, X_1 = x_1) = \mathbb{P}(X_s = x_0, X_{s+1} = x_1), \forall s \ge 0, \forall x_0, x_1 \in \mathcal{X}$. 

---

**Prop. 2:** Se $\pi$ é dist. estacionária para $(X_t)_{t \ge 0}$, então a cadeia $(X_t)_{t \ge 0}$ é um **processo estacionário** sob $\mathbb{P}_\pi$.

**Prova:**  

$$
\begin{aligned}
\mathbb{P}_\pi(X_0 = x_0, X_1 = x_1, \dots, X_t = x_t) &= \mathbb{P}_\pi(X_0 = x_0, \dots, X_{t-1} = x_{t-1}) \mathbb{P}_\pi(X_t = x_t \mid X_{t-1} = x_{t-1}, \dots, X_0 = x_0) \\
&= \mathbb{P}_\pi(X_0 = x_0, \dots, X_{t-1} = x_{t-1}) P(x_{t-1}, x_t) \\
&= \mathbb{P}_\pi(X_0 = x_0, \dots, X_{t-2} = x_{t-2}) P(x_{t-2}, x_{t-1}) P(x_{t-1}, x_t) \\
&\vdots \\
&= \mathbb{P}_\pi(X_0 = x_0) P(x_0, x_1) \dots P(x_{t-1}, x_t) \\
&= \pi(x_0) \prod_{n=1}^{t} P(x_{n-1}, x_n)
\end{aligned}
$$

De modo similar:  

$$
\begin{aligned}
\mathbb{P}_\pi(X_s = x_0, \dots, X_{s+t} = x_t) &= \mathbb{P}_\pi(X_s = x_0, \dots, X_{s+t-1} = x_{t-1}) \mathbb{P}_\pi(X_{t+s} = x_t \mid X_{s+t-1} = x_{t-1}, \dots, X_s = x_0) \\
&= \mathbb{P}_\pi(X_s = x_0, \dots, X_{s+t-1} = x_{t-1}) P(x_{t-1}, x_t) \\
&= \mathbb{P}_\pi(X_s = x_0) \prod_{n=1}^{t} P(x_{n-1}, x_n) \\
&= \pi(x_0) \prod_{n=1}^{t} P(x_{n-1}, x_n)
\end{aligned}
$$  
