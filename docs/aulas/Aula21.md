# Aula 21

**Data:** 08/05/2026

## Resumo: Amostrador de Gibbs

$\mathcal{X} = S^V = \{x = (x_v)_{v \in V} : x_v \in S, \, \forall v \in V\}$

$\pi$ med. de prob. em $\mathcal{X}$ t.q. $\forall v \in V$,

Conhecemos $\pi^{x,v}$, onde $\forall x \in \mathcal{X}$

$$\pi^{x,v}(y) = \begin{cases} 
0 & \text{se } y \notin \mathcal{X}(x,v) \\ \\
\dfrac{\pi(y)}{\displaystyle\sum_{z \in \mathcal{X}(x,v)} \pi(z)} & \text{se } y \in \mathcal{X}(x,v) 
\end{cases}$$

onde $\mathcal{X}(x,v) = \{y \in \mathcal{X} : y_u = x_u, \, \forall u \neq v\}$

---

### Dinâmica da Cadeia

Suponha que a Cadeia esteja no estado $x$, e aplique a seguinte regra para atualizar essa configuração:

1. Escolha $v \in V$ uniformemente ao acaso
2. Gere uma configuração de acordo com a distribuição $\pi^{x,v}$.

---

### Exemplo: (Modelo de Ising)

$\mathcal{X} = \{-1, +1\}^V$, onde $V$ é o conjunto de vértices de um grafo $G = (V,E)$. Neste exemplo, $S = \{-1, +1\}$ e o valor $x_v$ é chamado o **spin** em $v$.

Para cada $x \in \{-1, +1\}^V$, $H(x) = -\displaystyle\sum_{\substack{u,v \in V \\ u \sim v}} x_u x_v$  *(Energia / Hamiltoniano)*

**Distribuição de Gibbs:**

$$\pi(x) = \frac{\text{Exp}\{-\beta H(x)\}}{Z_\beta} , \text{ onde}$$

$\beta \ge 0$ e $Z_\beta = \displaystyle\sum_{y \in \mathcal{X}} \text{Exp}\{-\beta H(y)\}$ *(Função de Partição)*

$\beta :=$ como o inverso da temperatura

>  $\beta = 0 \Rightarrow$ Temperatura ser grande

>  Temperatura pequena $\Rightarrow \beta$ grande

---

$$\pi^{x,v}(y) = \frac{\pi(y)}{\displaystyle\sum_{z \in \mathcal{X}(x,v)} \pi(z)} \quad \text{para } y \in \mathcal{X}(x,v)$$

Como $\mathcal{X}(x,v) = \{x, x^{(v)}\}$, onde $x^{(v)} \in \mathcal{X}$ dada por:

$$x_u^{(v)} = \begin{cases} 
x_u & , \, u \neq v \\ 
-x_v & , \, u = v 
\end{cases}$$

Para $y = x$:

$$\pi^{x,v}(y) = \frac{\pi(x)}{\pi(x) + \pi(x^{(v)})} = \frac{\text{Exp}\{-\beta H(x)\}}{\text{Exp}\{-\beta H(x)\} + \text{Exp}\{-\beta H(x^{(v)})\}}$$

$$= \frac{1}{1 + \text{Exp}\{\beta (H(x) - H(x^{(v)}))\}}$$

---

Note que,

$$H(x) - H(x^{(v)}) = -\sum_{\substack{u,w \in V \\ u \sim w}} \left(x_u x_w - x_u^{(v)} x_w^{(v)}\right)$$

$$= -\sum_{\substack{u \sim v \\ u = v}} \sum_{w \sim u} \left(x_u x_w - x_u^{(v)} x_w^{(v)}\right)$$

$$= -\left[ \sum_{u \sim v} (x_u x_v - x_u(-x_v)) + \sum_{w \sim v} (x_v x_w - (-x_v) x_w) \right]$$

$$= -\left[ 2\sum_{u \sim v} x_u x_v + 2\sum_{w \sim v} x_v x_w \right]$$

$$= -4\sum_{u \sim v} x_u x_v$$

$$\Rightarrow \pi^{x,v}(x) = \frac{1}{1 + \text{Exp}\{-\beta \displaystyle\sum_{u \sim v} x_u x_v \}}$$

e

$$\pi^{x,v}(x^{(v)}) = \frac{\text{Exp}\{-\beta \displaystyle\sum_{u \sim v} x_u x_v \}}{1 + \text{Exp}\{-\beta \displaystyle\sum_{u \sim v} x_u x_v \}}$$

---

## Estados Recorrentes vs. Transientes

Seja $(X_t)_{t \ge 0}$ uma Cadeia de Markov com espaço de estados $\mathcal{X}$ **enumerável** e matriz de transição $P$.

$Def.:$ Um estado $x \in \mathcal{X}$ é **recorrente** se:

$$\mathbb{P}_x(\mathcal{T}_x^+ < \infty) = 1$$

E **transiente** caso contrário:

$$\left(\text{isto é, } \mathbb{P}_x(\mathcal{T}_x^+ < \infty) < 1\right),$$

onde $\mathcal{T}_x^+ = \min\{t \ge 1 : X_t = x\}$.

Além disso, um estado recorrente é chamado:

* **recorrente positivo** se $\mathbb{E}_x[\mathcal{T}_x^+] < \infty$, e
* **recorrente nulo** se $\mathbb{E}_x[\mathcal{T}_x^+] = \infty$.

---

**Exemplo:** $\mathcal{X} = \mathbb{N}$ 

$$P(x,y) = \begin{cases} 
p_x & \text{se } y = 0 \\ 
1 - p_x & \text{se } y = x + 1 \\ 
0 & \text{c.c.} 
\end{cases}$$

*$\hookrightarrow$ Uma cadeia irredutível* 

Com $0 < p_x < 1$.

Vamos estudar o comportamento do estado 0: 

Note que $\mathbb{P}_0(\mathcal{T}_0^+ = n) = (1 - p_0)(1 - p_1) \dots (1 - p_{n-2})p_{n-1}, \quad \forall n \ge 1$.  

Denote $u_0 = 1$ e $u_n = (1 - p_0) \dots (1 - p_{n-1}), \quad \forall n \ge 1$.

$$\begin{aligned}
\sum_{n=1}^{m} \mathbb{P}_0(\mathcal{T}_0^+ = n) &= \sum_{n=1}^{m} (u_{n-1} - u_n) \\
&= (u_0 - u_1) + (u_1 - u_2) + \dots + (u_{m-1} - u_m) \\
&= 1 - u_m
\end{aligned}$$

---

Logo, 

$$\begin{aligned}
\mathbb{P}_0(\mathcal{T}_0^+ < \infty) &= \sum_{n=1}^{\infty} \mathbb{P}_0(\mathcal{T}_0^+ = n) = \lim_{m \to \infty} \sum_{n=1}^{m} \mathbb{P}_0(\mathcal{T}_0^+ = n) \\
&= \lim_{m \to \infty} (1 - u_m) = 1 - \lim_{m \to \infty} u_m
\end{aligned}$$

---

$$\mathbb{P}_0(\mathcal{T}_0^+ < \infty) = 1 \iff$$

$$0 = \lim_{m \to \infty} u_m = \lim_{m \to \infty} \prod_{n=0}^{m-1} (1 - p_n) = \prod_{n=0}^{\infty} (1 - p_n)$$

$$\iff \sum_{n=0}^{\infty} p_n = \infty (Exercício)$$

**Ex.:** 

* $p_n = \dfrac{1}{n} \implies 0$ recorrente
* $p_n = \dfrac{1}{n^{1+\varepsilon}} \implies 0$ transiente

 *$\hookrightarrow$ A depender da escolha temos transiência e recorrência*

!!! info "Simulação Interativa Disponível"
    [Acessar Simulador :material-open-in-new:](../simulacoes/ising_simulator.html){: .md-button target="_blank" }

