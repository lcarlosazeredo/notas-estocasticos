# Aula 35

**Data:** 15/06/2026

## Irredutibilidade e Recorrência

Seja $X = (X_t)_{t \ge 0}$ uma Cadeia de Markov em tempo contínuo com matriz geradora $Q$.

**$Def.:$** $X$ é **irredutível** se, $\forall$ $x, y \in \mathcal{X}$, existe $t = t(x,y) \in [0, \infty)$ tal que $P_t(x,y) > 0$.

### Proposição 1
$X$ é irredutível $\iff$ $\forall$ $x, y \in \mathcal{X}$, existem $x_0 = x, x_1, \dots, x_m = y \in \mathcal{X}$ tais que $Q(x_{k}, x_{k+1}) > 0$ para todo $0 \le k \le m-1$.

---

Para cada $x \in \mathcal{X}$, denotamos o tempo total gasto no estado $x$ por:

$$N_x = \int_{0}^{J} \mathbb{1}_{\{X_t = x\}} dt$$

Onde $J = \lim_{n \to \infty} \tilde{S}_n$, com $\tilde{S}_n$ denotando os instantes de salto da cadeia.

**$Def.:$** O estado $x$ é **recorrente** se $P_x(N_x = \infty) = 1$. Caso contrário, $x$ é dito **transiente**.

### Proposição 2
$X$ é **recorrente** $\iff$ a sua cadeia imersa é **recorrente**.

---

Para cada $x \in \mathcal{X}$, denotamos o tempo da primeira passagem pelo estado $x$ por:

$$\mathcal{T}_{x,x}^{+} = \inf\{t \ge \tilde{S}_1 : X_t = x\}$$

Onde $\tilde{S}_1 = \inf\{t > 0 : X_t \neq X_0\}$.

Podemos provar que o estado $x \in \mathcal{X}$ é **recorrente** $\iff \mathbb{P}_x(\mathcal{T}_{x,x}^{+} < \infty) = 1$.

* O estado $x \in \mathcal{X}$ é **recorrente nulo** quando $\mathbb{P}_x(\mathcal{T}_{x,x}^{+} < \infty) = 1$ mas $\mathbb{E}_x[\mathcal{T}_{x,x}^{+}] = \infty$.
* Se $\mathbb{E}_x[\mathcal{T}_{x,x}^{+}] < \infty$, dizemos que $x$ é **recorrente positivo**.

---

### Teorema 1
Suponha $X$ **irredutível**, então as seguintes afirmações são equivalentes:

1. Cada $x \in \mathcal{X}$ é **recorrente positivo**.
2. Algum estado $x \in \mathcal{X}$ é **recorrente positivo**.
3. $X$ não tem explosões (i.e., $\mathbb{P}_x(J = \infty) = 1, \forall x$) e possui uma distribuição estacionária.

Além disso, se $\pi_X$ for uma distribuição estacionária, então:

$$\pi_X(x) = \frac{1}{\lambda_x \mathbb{E}_x[\mathcal{T}_{x,x}^{+}]}$$

---

#### Prova do Teorema 1

Antes de provar este teorema, vamos introduzir algumas notações. Para $x_0 \in \mathcal{X}$ fixado, defina:

$$\tilde{\pi}_X(x) = \mathbb{E}_{x_0} \left[ \int_{0}^{\mathcal{T}_{x,x_0}^{+} \wedge J} \mathbb{1}_{\{X_t = x\}} dt \right], \quad \forall x \in \mathcal{X}$$

Observe que:

$$\tilde{\pi}_X(x_0) = \mathbb{E}_{x_0}[\tilde{S}_1] = \mathbb{E}_{x_0}\left[\frac{1}{\lambda(x_0)} \mathcal{T}_1\right] = \frac{1}{\lambda(x_0)} \mathbb{E}_{x_0}[\mathcal{T}_1] = \frac{1}{\lambda(x_0)}$$

Além disso,

$$\sum_{x \in \mathcal{X}} \tilde{\pi}_X(x) = \sum_{x \in \mathcal{X}} \mathbb{E}_{x_0} \left[ \int_{0}^{\mathcal{T}_{x,x_0}^{+} \wedge J} \mathbb{1}_{\{X_t = x\}} dt \right]$$

$$= \mathbb{E}_{x_0} \left[ \int_{0}^{\mathcal{T}_{x,x_0}^{+} \wedge J} \sum_{x \in \mathcal{X}} \mathbb{1}_{\{X_t = x\}} dt \right]$$

$$= \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+} \wedge J]$$

Como $X_t = \tilde{Z}_n$ para $S_n \le t < S_{n+1}$, podemos escrever:

$$\int_{0}^{\mathcal{T}_{x,x_0}^{+} \wedge J} \mathbb{1}_{\{X_t = x\}} dt = \sum_{n=0}^{\infty} \tilde{\tau}_{n+1} \mathbb{1}_{\{\tilde{Z}_n = x, \mathcal{T}_{\tilde{Z},x_0}^{+} > n\}}$$

Logo,

$$\tilde{\pi}_X(x) = \sum_{n=0}^{\infty} \mathbb{E}_{x_0} \left[ \tilde{\tau}_{n+1} \mathbb{1}_{\{\tilde{Z}_n = x, \mathcal{T}_{\tilde{Z},x_0}^{+} > n\}} \right]$$

$$= \sum_{n=0}^{\infty} \mathbb{P}(\tilde{Z}_n = x, \mathcal{T}_{\tilde{Z},x_0}^{+} > n) \mathbb{E}_{x_0} \left[ \tilde{\tau}_{n+1} \mid \tilde{Z}_n = x, \mathcal{T}_{\tilde{Z},x_0}^{+} > n \right]$$

$$= \sum_{n=0}^{\infty} \mathbb{P}(\tilde{Z}_n = x, \mathcal{T}_{\tilde{Z},x_0}^{+} > n) \mathbb{E}_x \left[ \frac{1}{\lambda_x} T_{n+1} \right]$$

$$= \sum_{n=0}^{\infty} \mathbb{P}(\tilde{Z}_n = x, \mathcal{T}_{\tilde{Z},x_0}^{+} > n) \frac{1}{\lambda_x} = \frac{1}{\lambda_x} \tilde{\pi}_\tilde{Z}(x)$$

Onde $\tilde{\pi}_\tilde{Z}(x) = \mathbb{E}_{x_0} \left[ \sum_{n=0}^{\mathcal{T}_{\tilde{Z},x_0}^{+}} \mathbb{1}_{\{\tilde{Z}_n = x\}} \right]$ é a medida invariante da cadeia imersa.

Em conclusão, temos:

$$\tilde{\pi}_X(x) = \frac{1}{\lambda_x} \tilde{\pi}_\tilde{Z}(x) \quad \text{e} \quad \sum_{x \in \mathcal{X}} \tilde{\pi}_X(x) = \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+} \wedge J]$$

---

#### Prova:

**$(1) \implies (2)$:** Claro.

**$(2) \implies (3)$:** Suponha que $x_0 \in \mathcal{X}$ seja **recorrente positivo**. Pela Proposição 2, $x_0$ é recorrente positivo para a cadeia imersa, e portanto temos que $\mathbb{P}(J = \infty) = 1$, isto é, $X$ não tem explosões.

Consequentemente,

$$\sum_{x \in \mathcal{X}} \tilde{\pi}_X(x) = \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+} \wedge J] = \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+}] < \infty$$

Como $\tilde{\pi}_\tilde{Z}(\tilde{P} - I) = 0$, temos:

$$0 = \tilde{\pi}_\tilde{Z}(\tilde{P} - I) = \tilde{\pi}_X \Lambda (\tilde{P} - I) = \tilde{\pi}_X Q$$

Portanto, $\tilde{\pi}_X$ é uma medida estacionária para a cadeia a tempo contínuo. Definindo $\pi_X$ como a medida de probabilidade estacionária normalizada:

$$\pi_X = \frac{\tilde{\pi}_X}{\mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+}]}$$

Temos que:

$$\pi_X(x_0) = \frac{\tilde{\pi}_X(x_0)}{\mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+}]} = \frac{\frac{1}{\lambda_{x_0}}}{\mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+}]} = \frac{1}{\lambda_{x_0} \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^{+}]}$$
