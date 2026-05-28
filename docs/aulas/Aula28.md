# Aula 28

**Data:** 25/05/2026

## Processo de Poisson Composto

Seja $N = (N(t))_{t \ge 0}$ um Processo Pontual de Poisson de taxa $\lambda$ ($PPP(\lambda)$) e $Y = (Y_i)_{i \ge 1}$ uma sequência i.i.d., que também é independente de $N$.

Para cada $t \ge 0$, defina:

$$X_t = \sum_{i=1}^{N(t)} Y_i$$

Com a convenção de que $\sum_{i=1}^{\infty} Y_i = 0$. O processo $X = (X_t)_{t \ge 0}$ é chamado de **Processo de Poisson Composto**.

**Perguntas:**

1. $\mathbb{E}[X_t] = ?$
2. $\text{Var}(X_t) = ?$

---

### Proposição 1
Seja $(Y_i)_{i \ge 1}$ uma sequência i.i.d. e $N$ v.a. tomando valores em $\mathbb{N}$. Defina $X = \sum_{i=1}^{N} Y_i$ com a convenção de que $X = 0$ se $N = 0$. As seguintes propriedades valem:

**(i)** Se $\mathbb{E}[|Y_1|] < \infty$ e $\mathbb{E}[N] < \infty$, então:
$\mathbb{E}[X] = \mathbb{E}[N]\mathbb{E}[Y_1]$

**(ii)** Se $\mathbb{E}[Y_1^2] < \infty$ e $\mathbb{E}[N^2] < \infty$, então:
$\text{Var}(X) = \mathbb{E}[N]\text{Var}(Y_1) + \text{Var}(N)(\mathbb{E}[Y_1])^2$

**(iii)** Se $\mathbb{E}[Y_1^2] < \infty$ e $N \sim \text{Poi}(\lambda)$, então:
$\text{Var}(X) = \lambda \mathbb{E}[Y_1^2]$

---

### Prova da Proposição 1

#### **Item (i)**
Usando a propriedade da esperança condicional e a lei da probabilidade total:

$$\mathbb{E}[X] = \sum_{n=0}^{\infty} \mathbb{P}(N = n) \mathbb{E}[X | N = n]$$

Pela independência e linearidade da esperança:

$$\mathbb{E}\left[\sum_{i=1}^{n} Y_i \middle| N = n\right] = \mathbb{E}\left[\sum_{i=1}^{n} Y_i\right] = n\mathbb{E}[Y_1]$$

Logo,

$$\mathbb{E}[X] = \sum_{n=0}^{\infty} \mathbb{P}(N = n) n \mathbb{E}[Y_1] = \mathbb{E}[N]\mathbb{E}[Y_1]$$

*Alternativamente,*

$$\mathbb{E}[X|N] = f(N), \quad \text{onde } f(n) = \mathbb{E}[X|N=n] = n\mathbb{E}[Y_1]$$

$$\mathbb{E}[X|N] = N\mathbb{E}[Y_1] \implies \mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X|N]] = \mathbb{E}[N\mathbb{E}[Y_1]] = \mathbb{E}[N]\mathbb{E}[Y_1]$$

#### **Item (ii)**
Pela fórmula da variância condicional:

$$\text{Var}(X) = \mathbb{E}[\text{Var}(X|N)] + \text{Var}(\mathbb{E}[X|N])$$

Como $\mathbb{E}[X|N] = N\mathbb{E}[Y_1]$, então:

$$\text{Var}(\mathbb{E}[X|N]) = (\mathbb{E}[Y_1])^2 \text{Var}(N)$$

Observe que $\text{Var}(X|N) = V(N)$, onde $V(n) = \text{Var}(X|N=n)$:

$$= \text{Var}\left(\sum_{i=1}^{n} Y_i \middle| N = n\right) = \text{Var}\left(\sum_{i=1}^{n} Y_i\right) = n \text{Var}(Y_1)$$

$$\implies \text{Var}(X|N) = N \text{Var}(Y_1) \implies \mathbb{E}[\text{Var}(X|N)] = \mathbb{E}[N]\text{Var}(Y_1)$$

#### **Item (iii)**
Se $N \sim \text{Poi}(\lambda)$, então $\mathbb{E}[N] = \text{Var}(N) = \lambda$. Desse modo:

$$\text{Var}(X) = \lambda \left( \text{Var}(Y_1) + (\mathbb{E}[Y_1])^2 \right)$$

Como $\text{Var}(Y_1) = \mathbb{E}[Y_1^2] - (\mathbb{E}[Y_1])^2$, então:

$$\text{Var}(X) = \lambda \mathbb{E}[Y_1^2]$$

---

Usando os resultados da Proposição 1, obtemos que:

1. $\mathbb{E}[X_t] = \mathbb{E}[N(t)]\mathbb{E}[Y_1] = \lambda t \mathbb{E}[Y_1]$
2. $\text{Var}(X_t) = \lambda t \mathbb{E}[Y_1^2]$

> **Propriedade útil:**
>
> * $\text{Var}(X) = \mathbb{E}[\text{Var}(X|Y)] + \text{Var}(\mathbb{E}[X|Y])$
> * $\text{Var}(\mathbb{E}[X|Y]) = \mathbb{E}[(\mathbb{E}[X|Y])^2] - (\mathbb{E}[\mathbb{E}[X|Y]])^2 = \mathbb{E}[(\mathbb{E}[X|Y])^2] - (\mathbb{E}[X])^2$
> * $\mathbb{E}[\text{Var}(X|Y)] = \mathbb{E}[\mathbb{E}[X^2|Y] - (\mathbb{E}[X|Y])^2] = \mathbb{E}[X^2] - \mathbb{E}[(\mathbb{E}[X|Y])^2]$

---

## Processo de Poisson Não-Homogêneo

Seja $\lambda: [0, \infty) \rightarrow [0, \infty)$ uma função tal que $\lambda(t) \le \bar{\lambda}$, para todo $t \ge 0$, onde $\bar{\lambda} > 0$.

Dizemos que um processo de contagem $N = (N(t))_{t \ge 0}$ é um **$PPP(\lambda)$ não-homogêneo** se:

1. $N(0) = 0$.
2. $N([a,b]) \sim \text{Poi}\left(\int_{a}^{b} \lambda(t) dt\right)$.
3. As variáveis $N([a_i, b_i])$ são independentes para todos intervalos $[a_i, b_i]$ ($i = 1, \dots, n$) que sejam disjuntos dois a dois.


Construção:

Simule um $PPP(\bar{\lambda})$ e para cada evento $S_n = t$ deste processo, inclua no Processo Não-Homogêneo com probabilidade $\frac{\lambda(t)}{\bar{\lambda}}$

---

## Filas $M/G/\infty$

Modela o tamanho de uma fila por unidade de tempo, baseado nas seguintes condições:

1. Os clientes são atendidos por um número fixo $k$ de servidores, $k \in \mathbb{N} \cup \{\infty\}$, que atendem um cliente por vez.
2. Os tempos entre chegadas consecutivas de clientes são i.i.d. .
3. Os tempos de serviços são i.i.d. .
4. Os tempos de chegadas são independentes dos tempos de serviço.

### Nomenclatura:
* **M**: Tempos exponenciais.
* **G**: Qualquer distribuição em $(0, \infty)$
* **$k$**: Número de servidores.

### Exemplo
Considere $(X_t)_{t \ge 0}$ uma fila $M/G/\infty$ com taxa de chegada de clientes $\lambda > 0$ e função de distribuição dos tempos de serviço $F$.

Defina $(N(t))_{t \ge 0}$ o $PPP(\lambda)$ que conta o número de clientes que chegam na fila e $(Y_t)_{t \ge 0}$ o Processo que conta o número de clientes atendidos.

Assim,

$$X_t + Y_t = N(t)$$

**Perguntas:**

1. $X_t \sim$ ? e $Y_t \sim$ ?
2. $X_t$ e $Y_t$ são independentes?

---

### Proposição 2
Para todo $t > 0$, $X_t$ e $Y_t$ são independentes e:

$$X_t \sim \text{Poi}\left(\lambda \int_{0}^{t} (1 - F(u)) du\right)$$

$$Y_t \sim \text{Poi}\left(\lambda \int_{0}^{t} F(u) du\right)$$

#### **Prova:**
Fixe $t > 0$ e tome $n \ge 1$. 

Dado que ocorreu um total de $N(t) = n$ chegadas, os tempos das chegadas(sem levar em conta a origem) são variáveis aleatórias i.i.d. com **distribuição Uniforme** em $[0, t]$.

Denote esses instantes de chegada por $U_1, \dots, U_n$ e por $W_1, \dots, W_n$ seus respectivos tempos de atendimento. Por hipótese, as variáveis aleatórias $(U_j : j = 1, \dots, n)$ e $(W_j : j = 1, \dots, n)$ são independentes.

O cliente que chegou no tempo $U_j$ ainda estará na fila no tempo $t$ com probabilidade:

$$\mathbb{P}(W_j > t - U_j) = \mathbb{P}(W_1 > t - U_1) = \int_{0}^{t} \frac{1}{t} \mathbb{P}(W_1 > t - U_1 | U_1 = s) ds$$

$$= \frac{1}{t} \int_{0}^{t} \mathbb{P}(W_1 > t - s) ds = \frac{1}{t} \int_{0}^{t} (1 - F(t - s)) ds$$

