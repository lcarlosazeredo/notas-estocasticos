# Aula 33

**Data:** 08/06/2026

## Revisão:

Dada uma matriz geradora $Q = (Q(x,y))_{x,y \in \mathcal{X}}$ tal que:

1. $Q(x,y) \ge 0, \quad \forall x \neq y$
2. $Q(x,x) = -\lambda(x)$, com $\lambda(x) = \sum_{y \neq x} Q(x,y) < \infty, \quad \forall x \in \mathcal{X}$

Definimos, $\forall t \ge 0$:

$$X_t = \begin{cases} \tilde{Z}_0, & \text{se } 0 \le t < \tilde{S}_1 \\ \tilde{Z}_n, & \text{se } t \in \bigcup_{n=1}^{\infty} [\tilde{S}_n, \tilde{S}_{n+1}) \end{cases}$$

Onde $(\tilde{Z}_n)_{n \ge 0}$ é a **Cadeia Imersa** com matriz de transição $\tilde{P} = (\tilde{P}(x,y))_{x,y \in \mathcal{X}}$ dada por:

$$\tilde{P}(x,y) = \begin{cases} \frac{Q(x,y)}{\lambda(x)}, & \text{se } x \neq y \\ 0, & \text{se } x = y \end{cases}$$


Os instantes de salto são definidos por:

$$\tilde{S}_n = \tilde{\mathcal{T}}_1 + \dots + \tilde{\mathcal{T}}_n$$

Com $\tilde{\mathcal{T}}_n = \frac{\mathcal{T}_n}{\lambda(\tilde{Z}_{n-1})}$, onde $(\mathcal{T}_i)_{i \ge 1}$ é uma sequência de variáveis aleatórias i.i.d. com distribuição $Exp(1)$, independentes da cadeia imersa $(\tilde{Z}_n)_{n \ge 0}$.

Dessa forma, as probabilidades de transição de $P_t = (P_t(x,y))_{x,y \in \mathcal{X}}$ são dadas por $P_t(x,y) = \mathbb{P}(X_t = y \mid X_0 = x)$.

---

## Condição de Regularidade

Esta construção está bem definida se, com probabilidade 1, a cadeia não der infinitos saltos em um tempo finito. Ou seja:

$$\lim_{n \to \infty} \tilde{S}_n = \infty \quad (\star)$$

Sob esta condição, vimos que:

$$\lim_{t \to 0} \frac{P_t(x,y)}{t} = Q(x,y), \quad x \neq y \qquad \text{e} \qquad \lim_{t \to 0} \frac{P_t(x,x) - 1}{t} = -\lambda(x)$$

Uma Cadeia de Markov em tempo contínuo construída da forma acima e que satisfaz a Condição ($\star$) é chamada de **Regular**.

---

## Proposição 1

Sejam $(\hat{\mathcal{T}}_n)_{n \ge 1}$ variáveis aleatórias independentes tais que $\hat{\mathcal{T}}_n \sim Exp(\alpha_n)$, com $\alpha_n \in (0, \infty)$. Então:

**(a)** $\mathbb{P}\left(\sum_{n=1}^{\infty} \hat{\mathcal{T}}_n < \infty\right) \in \{0,1\}$

**(b)** $\mathbb{P}\left(\sum_{n=1}^{\infty} \hat{\mathcal{T}}_n < \infty\right) = 1 \iff \sum_{n=1}^{\infty} \frac{1}{\alpha_n} < \infty$

> **Corolário:** A Condição ($\star$) vale para uma condição inicial $x$
>
> $$\iff \mathbb{P}_x \left( \sum_{n=0}^{\infty} \frac{1}{\lambda(\tilde{Z}_n)} < \infty \right) = 0$$

Se $\sup_{x \in \mathcal{X}} \lambda(x) = \bar{\lambda} < \infty$, então $\mathbb{P}\left(\sum_{n=1}^{\infty} \hat{\mathcal{T}}_n < \infty\right) = 0$:

$$\mathbb{E}[\tilde{\mathcal{T}}_n \mid \tilde{Z}_{n-1}] = \frac{1}{\lambda(\tilde{Z}_{n-1})} \ge \frac{1}{\bar{\lambda}} > 0 \implies \sum_{n=1}^{\infty} \frac{1}{\alpha_n} = \infty$$

Observe que se escrevermos $\Lambda = \text{diag}((\lambda(x))_{x \in \mathcal{X}})$, então a matriz geradora pode ser expressa como:

$$Q = \Lambda(\tilde{P} - I)$$

---

## Processo de Nascimento

Considere o espaço de estados $\mathcal{X} = \{1, 2, \dots\}$. As taxas de transição são definidas por:

$$Q(x, x+1) = \beta_x \quad \text{e} \quad Q(x,y) = 0 \quad, se x \neq y$$

Portanto, a taxa total de saída $\lambda(x) = \beta_x$, e as probabilidades de transição da cadeia imersa são:

$$\tilde{P}(x,y) = \begin{cases} 1, & \text{se } y = x + 1 \\ 0, & \text{c.c.} \end{cases}$$


Quando $\beta_x = \beta x, \quad \forall x \in \{1, 2, \dots\}$ e $\beta >0$, o processo de nascimento é chamado de Yule.

Para este exemplo, podemos calcular $P_t$.

### Afirmação:
**(i)** $P_t(1,y) = e^{-\beta t}(1 - e^{-\beta t})^{y-1}, \quad y \ge 1$  
**(ii)** $P_t(x,y) = \binom{y-1}{x-1} e^{-\beta t x}(1 - e^{-\beta t})^{y-x}, \quad y \ge x \ge 1$

#### Verificação de (i):
O tempo do $n$-ésimo nascimento pode ser escrito como $\tilde{S}_n = W_1 + \dots + W_n$, onde $W_1 , \dots , W_n$ são independentes e para cada $x \in \mathcal{X}$, $W_x \sim Exp(\beta x)$.

**Fato:** Sejam $E_1, \dots, E_n$ v.a. i.i.d. com distribuição $Exp(\beta)$ e sejam $E_{(1)} < E_{(2)} < \dots < E_{(n)}$ as suas estatísticas de ordem correspondentes. Então, os incrementos $E_{(1)}, E_{(2)} - E_{(1)}, \dots, E_{(n)} - E_{(n-1)}$ são v.a. independentes tais que:

$$E_{(1)} \sim Exp(n\beta) \quad \text{e} \quad E_{(i+1)} - E_{(i)} \sim Exp((n-i)\beta), \forall 1 < i < n-1$$

$$\Rightarrow P_t(1,n) = \mathbb{P}(E_{(n-1)} \le t < E_{(n)})$$

$$= \mathbb{P}(E_{(n-1)} \le t) - \mathbb{P}(E_{(n)} \le t)$$

$$= (1 - e^{-\beta t})^{n-1} - (1 - e^{-\beta t})^n$$

$$= (1 - e^{-\beta t})^{n-1} \Big[ 1 - (1 - e^{-\beta t}) \Big]$$

$$= (1 - e^{-\beta t})^{n-1} e^{-\beta t}$$