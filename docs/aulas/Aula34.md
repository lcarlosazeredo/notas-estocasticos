# Aula 34

**Data:** 10/06/2026

## Equações de Kolmogorov

Dado $Q = (Q(x,y))_{x,y \in \mathcal{X}}$ uma matriz geradora tal que:

1. $Q(x,y) \ge 0, \quad \forall x \neq y$
2. $0 \le -Q(x,x) < \infty$ e $\sum_{y \in \mathcal{X}} Q(x,y) = 0$

Construímos $(X_t)_{t \ge 0}$ tal que:

$$\lim_{t \to 0} \frac{P_t(x,y)}{t} = Q(x,y), \quad x \neq y$$

$$\lim_{t \to 0} \frac{P_t(x,x) - 1}{t} = Q(x,x)$$

Onde $P_t = (P_t(x,y))_{x,y \in \mathcal{X}}$ representa as probabilidades de transição, que satisfazem as Equações de Chapman-Kolmogorov:

$$P_{t+s} = P_t P_s = P_s P_t$$

Logo,

$$\frac{1}{s}(P_{t+s} - P_t) = \frac{1}{s}(P_t P_s - P_t) = P_t \frac{(P_s - I)}{s}$$

---

Tomando o limite quando $s \to 0$, obtemos:

### 1. Forward Equation (Equação Prospectiva)
$$\frac{dP_t}{dt} = \lim_{s \to 0} \frac{1}{s}(P_{t+s} - P_t) = \lim_{s \to 0} P_t \frac{(P_s - I)}{s} = P_t \left( \lim_{s \to 0} \frac{P_s - I}{s} \right) = P_t Q$$

### 2. Backward Equation (Equação Retrospectiva)
$$\frac{dP_t}{dt} = \lim_{s \to 0} \frac{1}{s}(P_{t+s} - P_t) = \lim_{s \to 0} \frac{(P_s - I)}{s} P_t = \left( \lim_{s \to 0} \frac{P_s - I}{s} \right) P_t = Q P_t$$

Note: $\tilde{P}_t = e^{tQ} = \sum_{n=0}^{\infty} \frac{(tQ)^n}{n!}$ satisfaz ambas as equações:

$$\frac{d\tilde{P}_t}{dt} = \frac{d}{dt} \left( \sum_{n=0}^{\infty} \frac{(tQ)^n}{n!} \right) = \sum_{n=1}^{\infty} \frac{n t^{n-1} Q^n}{n!}$$

$$= \sum_{n=1}^{\infty} \frac{t^{n-1}}{(n-1)!} Q^n = \left( \sum_{n=1}^{\infty} \frac{(tQ)^{n-1}}{(n-1)!} \right) Q = Q \left( \sum_{n=1}^{\infty} \frac{(tQ)^{n-1}}{(n-1)!} \right)$$

$$= e^{tQ} Q = Q e^{tQ}$$

Pela unicidade, temos que $P_t = e^{tQ}$.

---

Reescrevendo as equações $\forall x, y \in \mathcal{X}$:

* **Equação Prospectiva:**
  $\frac{d}{dt}P_t(x,y) = \sum_{z \in \mathcal{X}} P_t(x,z)Q(z,y) = \sum_{z \neq y} P_t(x,z)Q(z,y) + P_t(x,y)Q(y,y)$
  $= \sum_{z \neq y} \left[ P_t(x,z)Q(z,y) - P_t(x,y)Q(y,z) \right]$

* **Equação Retrospectiva:**
  $\frac{d}{dt}P_t(x,y) = \sum_{z \in \mathcal{X}} Q(x,z)P_t(z,y) = \sum_{z \neq x} Q(x,z)P_t(z,y) + Q(x,x)P_t(x,y)$
  $= \sum_{z \neq x} \left[ P_t(z,y) - P_t(x,y) \right] Q(x,z)$

---

### Exemplo: Processo de Nascimento Puro

Considere um processo com espaço de estados $\mathcal{X} = \{1, 2, 3, \dots\}$ e taxas de transição dadas por:

$$Q(x,y) = \begin{cases} \beta_x, & \text{se } y = x + 1 \\ -\beta_x, & \text{se } y = x \\ 0, & \text{c.c.} \end{cases}$$

Pela **Equação Prospectiva**, $\forall x, y$:

$$\frac{d}{dt}P_t(x,y) = P_t(x,y)Q(y,y) + P_t(x,y-1)Q(y-1,y) = -\beta_y P_t(x,y) + \beta_{y-1} P_t(x,y-1)$$

Para $y = x$, sabendo que $P_t(x, y) = 0$ para todo $y < x$, temos que:

$$\frac{d}{dt}P_t(x,x) = -\beta_x P_t(x,x) \implies P_t(x,x) = P_0(x,x)e^{-\beta_x t} = e^{-\beta_x t}$$

Então:

$$\frac{d}{dt} \left( P_t(x,y)e^{\beta_y t} \right) = e^{\beta_y t} \frac{d}{dt}P_t(x,y) + \beta_y e^{\beta_y t} P_t(x,y)$$

$$= e^{\beta_y t} \left( \frac{d}{dt}P_t(x,y) + \beta_y P_t(x,y) \right) = e^{\beta_y t} \beta_{y-1} P_t(x,y-1)$$

$$\Rightarrow P_t(x,y)e^{\beta_y t} - P_0(x,y)e^{\beta_y 0} = \int_{0}^{t} e^{\beta_y s} \beta_{y-1} P_s(x,y-1) ds$$

$\Rightarrow \forall x \neq y,$

$$P_t(x,y) = e^{-\beta_y t} \beta_{y-1} \int_{0}^{t} e^{\beta_y s} P_s(x,y-1) ds$$

Iterando, obtemos $P_t(x,y)$ para todo y.

> **Observação:** Para derivar rigorosamente as Equações de Chapman-Kolmogorov, precisamos supor que $\lim_{t \to 0} \frac{P_t - I}{t} = Q$ e que $-\sum_{y \in \mathcal{X}} P_t(x,y)Q(y,y) < \infty, \forall x \in \mathcal{X}$.

---

## Distribuição Estacionária

**$Def.:$** Seja $\pi = (\pi(x))_{x \in \mathcal{X}}$ um vetor de probabilidade em $\mathcal{X}$ é uma **distribuição estacionária** para a Cadeia de Markov com matriz geradora $Q$ se:

$$\pi P_t = \pi, \quad \forall t \ge 0$$

Denotando $\pi_t = \pi P_t$, vemos que 

$\pi$ é estacionária $\iff$ $\pi_t = \pi$, $\forall t \ge 0$

Logo,

$$\frac{d\pi_t}{dt} = \frac{d}{dt}(\pi P_t) = \pi \frac{dP_t}{dt} = \pi P_t Q = \pi_t Q$$

Para justificar, precisamos supor que $\sum_{y \in \mathcal{X}} \pi_t(y)Q(y,y) < \infty$.

### Teorema 1
$\pi$ é uma distribuição estacionária se e somente se:

$$\pi Q = 0$$

#### Prova:
1. **$(\implies)$** Se $\pi$ é estacionária, então $\pi_t = \pi$ para todo $t \ge 0$. Portanto, $\frac{d\pi_t}{dt} = 0$. Como $\frac{d\pi_t}{dt} = \pi_t Q$, temos $\pi Q = 0$.
2. **$(\impliedby)$** Se $\pi Q = 0$, então: $\frac{d\pi_t}{dt} = \pi \frac{dP_t}{dt} = \pi Q P_t = (\pi Q)P_t = 0 \cdot P_t = 0$

   $\qquad \Rightarrow \pi_t = \pi_0 = \pi, \forall t \ge 0$. Logo, $\pi$ é distribuição estacionária.

Note que $\pi Q = 0 \iff \forall y \in \mathcal{X}$:

$$\sum_{x \in \mathcal{X}} \pi(x)Q(x,y) = 0 \iff \sum_{x \neq y} \pi(x)Q(x,y) - \pi(y)Q(y,y) = 0$$

Obtemos:

$$\sum_{x \neq y} \pi(x)Q(x,y) = \pi(y) \sum_{x \neq y} Q(y,x)$$

---

### Exemplo:

Seja o espaço de estados $\mathcal{X} = \{1, 2\}$ e a matriz geradora:

$$Q = \begin{pmatrix} -\beta & \beta \\ \mu & -\mu \end{pmatrix}$$

Onde $Q(1,2) = \beta$ e $Q(2,1) = \mu$. Para encontrar a distribuição estacionária $\pi = (\pi(1), \pi(2))$, resolvemos o sistema:

$$\begin{cases} \pi Q = 0 \\ \pi(1) + \pi(2) = 1 \end{cases} \iff \begin{cases} -\beta\pi(1) + \mu\pi(2) = 0 \\ \pi(1) + \pi(2) = 1 \end{cases}$$

Obtemos:

$$\pi(1) = \frac{\mu}{\beta + \mu} \quad \text{e} \quad \pi(2) = \frac{\beta}{\beta + \mu}$$