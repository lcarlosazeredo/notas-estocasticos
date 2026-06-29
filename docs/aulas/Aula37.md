# Aula 37

**Data:** 19/06/2026

## Reversibilidade

**$Def.:$** Uma distribuição de probabilidade $\pi$ é **reversível** para uma Cadeia de Markov em tempo contínuo com matriz geradora $Q$ se:

$$\pi(x)Q(x,y) = \pi(y)Q(y,x), \quad \forall x, y \in \mathcal{X}$$

> **Interpretação:** $\pi(x)Q(x,y)$ representa o **fluxo probabilístico** do estado $x$ para o estado $y$. A condição de reversibilidade estabelece que o fluxo de $x \to y$ é igual ao fluxo de $y \to x$.

---

### Proposição 1
Se $\pi$ é **reversível** para $Q$, então $\pi Q = 0$

#### Prova:
Para qualquer $y \in \mathcal{X}$:

$$\pi Q(y) = \sum_{x \in \mathcal{X}} \pi(x)Q(x,y) = \sum_{x \neq y} \pi(x)Q(x,y) + \pi(y)Q(y,y)$$

Como $Q(y,y) = -\sum_{x \neq y} Q(y,x)$, substituímos na equação:

$$\pi Q(y) = \sum_{x \neq y} \pi(x)Q(x,y) - \pi(y)\sum_{x \neq y} Q(y,x)$$

$$\pi Q(y) = \sum_{x \neq y} \Big[ \pi(x)Q(x,y) - \pi(y)Q(y,x) \Big]$$

Pela hipótese de reversibilidade, $\pi(x)Q(x,y) - \pi(y)Q(y,x) = 0$ para todo $x \neq y$. Portanto:

$$\pi Q(y) = \sum_{x \neq y} 0 = 0$$

Como isso vale para todo $y$, temos $\pi Q = 0$.

---

### Proposição 2
Se $\pi$ é **reversível**, então a cadeia, sob a lei $\mathbb{P}_\pi$, é **reversível no tempo**. Mais precisamente, $\forall$ $T > 0$ fixado:

A distribuição do processo $(X_t)_{0 \le t < T}$ coincide com a distribuição de $(X_{T-t})_{0 \le t < T}$ sob $\mathbb{P}_\pi$.

---

## Exemplo: Cadeia de Nascimento e Morte

Considere uma Cadeia com:

* **Espaço de estados:** $\mathcal{X} = \{0, 1, \dots, N\}$, com $1 \le N \le \infty$.
* **Taxas de transição:** $\forall$ $1 \le x < N$, a matriz $Q$ é dada por:

$$Q(x,y) = \begin{cases} \beta_x, & \text{se } y = x+1 \\ \mu_x, & \text{se } y = x-1 \\ -(\beta_x + \mu_x), & \text{se } y = x \\ 0, & \text{c. c.} \end{cases}$$

Para as fronteiras $x = 0$ e $x = N$ (caso $N < \infty$):

$$Q(0,y) = \begin{cases} -\beta_0, & \text{se } y = 0 \\ \beta_0, & \text{se } y = 1 \\ 0, & \text{c. c.} \end{cases}$$

$$Q(N,y) = \begin{cases} \mu_N, & \text{se } y = N-1 \\ -\mu_N, & \text{se } y = N \\ 0, & \text{c. c.} \end{cases}$$

Onde $(\beta_x)_{x \ge 0}$ são as taxas de nascimento e $(\mu_x)_{x \ge 0}$ são as taxas de morte.


1. Vamos supor que $\beta_x > 0$ e $\mu_x > 0$ $\forall$ $x \in \mathcal{X}$ (quando fizer esentido).
2. Para evitar explosões, assumimos que $\sup_{x} (\mu_x + \beta_x) < \infty$.

---

**Dist. Estacionária:**

Queremos encontrar $\pi$ tal que $\pi Q = 0$, ou seja, $\sum_{x} \pi(x)Q(x,y) = 0$ para todo $y$.

* **Para $y = 0$:**

$$\pi(0)Q(0,0) + \pi(1)Q(1,0) = 0$$

$$\pi(0)(-\beta_0) + \pi(1)\mu_1 = 0 \implies \pi(1)\mu_1 = \pi(0)\beta_0$$

* **Para $y = 1$:**

$$\pi(0)Q(0,1) + \pi(1)Q(1,1) + \pi(2)Q(2,1) = 0$$

$$\pi(0)\beta_0 - \pi(1)(\beta_1 + \mu_1) + \pi(2)\mu_2 = 0$$
  
Substituindo $\pi(0)\beta_0 = \pi(1)\mu_1$:

$$\pi(1)\mu_1 - \pi(1)\mu_1 - \pi(1)\beta_1 + \pi(2)\mu_2 = 0 \implies \pi(2)\mu_2 = \pi(1)\beta_1$$

Procedendo por indução, deduzimos que para todo $0 \le y < N$:

$$(\star) \quad \pi(y+1)\mu_{y+1} = \pi(y)\beta_y$$

$\implies \pi$ é **reversível**

---

Iterando $(\star)$, obtemos que:

$$\pi(y) = \pi(y-1)\frac{\beta_{y-1}}{\mu_y} = \pi(y-2)\frac{\beta_{y-2}\beta_{y-1}}{\mu_{y-1}\mu_y}$$

Logo, para qualquer $y \ge 1$:

$$\pi(y) = \pi(0) \prod_{j=0}^{y-1} \frac{\beta_j}{\mu_{j+1}}$$

Para que $\pi$ seja uma medida de probabilidade, precisamos que $\sum_{y \in \mathcal{X}} \pi(y) = 1$. Portanto:

$$\pi(0) \left( 1 + \sum_{y=1}^{N} \prod_{j=0}^{y-1} \frac{\beta_j}{\mu_{j+1}} \right) = 1$$

Isso exige que $\sum_{y=1}^{N} \prod_{j=0}^{y-1} \frac{\beta_j}{\mu_{j+1}} < \infty$. Sob esta condição, o termo inicial $\pi(0)$ é:

$$\pi(0) = \frac{1}{1 + \sum_{y=1}^{N} \prod_{j=0}^{y-1} \frac{\beta_j}{\mu_{j+1}}}$$

---

### Caso Particular: Fila M/M/1

Se as taxas forem constantes, ou seja, $\beta_x = \beta$ e $\mu_x = \mu$ para todo $x$, com $N = \infty$ (Fila M/M/1):

$$\pi(y) = \left(\frac{\beta}{\mu}\right)^y \left(1 - \frac{\beta}{\mu}\right), \quad \text{para } \beta < \mu$$

---

### Prop.: Fila M/M/k

**Proposição:** Considere uma fila M/M/k em regime permanente (estacionário), onde os clientes chegam segundo um Processo de Poisson de taxa $\lambda$ e são atendidos por um dos $k$ servidores, cada um com taxa de atendimento exponencial $\mu$. As taxas do processo são:

$$\beta_x = \beta, \quad \forall x \ge 0$$

$$\mu_x = \begin{cases} x\mu, & \text{se } x < k \\ k\mu, & \text{se } x \ge k \end{cases}$$

O processo que marca os instantes de **saída dos clientes** após o término do atendimento é, sob a distribuição estacionária, também um **Processo de Poisson de taxa $\lambda$**.

1. No tempo normal (indo para frente), os instantes de chegada dos clientes formam um Processo de Poisson de taxa $\lambda$, fazendo o número de clientes $X_t$ crescer uma unidade ($+1$).
2. Como a cadeia é reversível sob a distribuição estacionária, se olharmos para o processo **andando para trás no tempo**, o comportamento estatístico é idêntico.
3. No tempo revertido, os saltos que eram decréscimos (saídas no tempo normal) passam a ser incrementos ($+1$ no tempo revertido).
4. Pela reversibilidade, esses incrementos no tempo revertido devem se comportar exatamente como as chegadas do tempo normal, ou seja, seguem a mesma lei exponencial e formam um Processo de Poisson de taxa $\lambda$. 
5. Consequentemente, os instantes de saída no tempo normal constituem um Processo de Poisson de taxa $\lambda$.

