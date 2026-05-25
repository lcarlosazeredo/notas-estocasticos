# Aula 27

**Data:** 22/05/2026

## Processos Pontuais

* **Instantes das chegadas/eventos:** $(S_n)_{n \ge 1}$
* **Processo de contagem:** $(N(t))_{t \ge 0}, N(t) = \sum_{n=1}^{\infty} \mathbb{1}_{\{S_n \le t\}}$

Se $T_1 = S_1$ e $T_n = S_n - S_{n-1}$, $n \ge 2$, então $(T_n)_{n \ge 1}$ é uma sequência i.i.d. com $T_i \sim \text{Exp}(\lambda)$.

Se $(N(t))_{t \ge 0}$ é $PPP(\lambda)$

Em particular, temos

$$S_n = \sum_{i=1}^{n} T_i \sim \text{Gama}(n, \lambda)$$

Isto é, $S_n$ é uma variável aleatória contínua com função densidade de probabilidade dada por:

$$f_{S_n}(t) = \lambda e^{-\lambda t} \frac{(\lambda t)^{n-1}}{(n-1)!} \mathbb{1}_{[0, \infty)}(t)$$

---

## Distribuição Condicional dos Tempos de Chegada

**Pergunta:** Fixo $t > 0$. Dado que $N(t) = n$, qual é a distribuição conjunta de $(S_1, \dots, S_n)$?

### Caso simples: $n = 1$
Fixe $0 < s < t$:

$$\mathbb{P}(S_1 \le s \mid N(t) > 1) = \frac{\mathbb{P}(N(s) = 1, N(t) = 1)}{\mathbb{P}(N(t) = 1)}$$

$$= \frac{\mathbb{P}(N(s) = 1, N((s, t]) = 0)}{\mathbb{P}(N(t) = 1)}$$

$$= \frac{\mathbb{P}(N(s) = 1) \mathbb{P}(N((s, t]) = 0)}{\mathbb{P}(N(t) = 1)}$$

$$= \frac{(e^{-\lambda s} \lambda s) \cdot (e^{-\lambda(t - s)})}{e^{-\lambda t} \lambda t} = \frac{s}{t} \frac{e^{-\lambda t}}{e^{-\lambda t}} = \frac{s}{t}$$

Logo, $S_1 \mid \{N(t) = 1\} \sim \text{Unif}((0, t))$.

---

### Caso Geral e Estatísticas de Ordem

Para analisar o caso geral, precisamos relembrar alguns fatos sobre as **estatísticas de ordem**.

Sejam $Y_1, \dots, Y_n$ variáveis aleatórias. Definimos as estatísticas de ordem como:

* $Y_{(1)} = \min\{Y_1, \dots, Y_n\}$
* $Y_{(i)} = \min(\{Y_1, \dots, Y_n\} \mid \{Y_{(1)}, \dots, Y_{(i-1)}\}), \quad i \ge 2$

Por definição, as variáveis transformadas ficam ordenadas: $Y_{(1)} \le Y_{(2)} \le \dots \le Y_{(n)}$.

> **Fato:** Se $Y_1, \dots, Y_n$ são i.i.d. contínuas com densidade $f$, a densidade conjunta das estatísticas de ordem $(Y_{(1)}, \dots, Y_{(n)})$ é dada por:
>
> $$f(y_1, \dots, y_n) = n! \prod_{i=1}^{n} f(y_i), \quad \text{se } y_1 < y_2 < \dots < y_n$$
>
> Caso contrário, $f(y_1, \dots, y_n) = 0$.

Em particular, se $Y_i \sim \text{Unif}((0, t))$, então $f(y_i) = \frac{1}{t}$. Portanto:

$$f(y_1, \dots, y_n) = \begin{cases} \frac{n!}{t^n}, & \text{se } y_1 < y_2 < \dots < y_n \\ 0, & \text{c.c.} \end{cases}$$

---

### Teorema 1
Dado que $N(t) = n$, temos que  $(S_1, \dots, S_n)$ têm a mesma distribuição que as estatísticas de ordem de $n$ variáveis aleatórias i.i.d. com distribuição Uniforme no intervalo $(0, t)$.

**Prova:**
Sejam $0 < t_1 < t_2 < \dots < t_n < t_{n+1} = t$ e $h_i > 0$ suficientemente pequenos tais que $t_i + h_i < t_{i+1}$.

Queremos calcular:

$$P(t_i \le S_i \le t_i + h_i, \; i = 1, \dots, n \mid N(t) = n)$$

$$= \frac{P\left( \bigcap_{i=1}^n \{N((t_i, t_i + h_i]) = 1\}, N(t_i)=0, \; \bigcap_{i=1}^n \{N((t_i + h_i, t_{i+1}]) = 0\} \right)}{P(N(t) = 0)}$$

$$= \frac{\prod_{i=1}^{n} \left( e^{-\lambda h_i} \lambda h_i \right) \cdot e^{-\lambda t}\cdot \prod_{i=1}^{n} e^{-\lambda(t_{i+1} - (t_i + h_i))}}{\frac{e^{-\lambda t} (\lambda t)^n}{n!}}$$

$$= n! \prod_{i=1}^{n} \left( \frac{h_i}{t} \right)$$

---

## Superposição de PPP

Sejam $(N^{(1)}(t))_{t \ge 0}, \dots, (N^{(k)}(t))_{t \ge 0}$ processos de Poisson independentes, cada um com taxa $\lambda_i$, para $i = 1, \dots, k$.

A **superposição** desses processos é o processo $(N(t))_{t \ge 0}$ onde:

$$N(t) = \sum_{i=1}^{k} N^{(i)}(t)$$

**Pergunta:** O processo $(N(t))_{t \ge 0}$ é um PPP?

### Teorema 2
A superposição $(N(t))_{t \ge 0}$ é um $PPP(\lambda)$, onde $\lambda = \sum_{i=1}^{k} \lambda_i$.

**Prova:**
Fixe um intervalo $[a, b]$

$$N([a, b]) = \sum_{i=1}^{k} N^{(i)}([a, b]) \sim \text{Poi}\left( \sum_{i=1}^{k} \lambda_i (b - a) \right) = \text{Poi}\left( \left(\sum_{i=1}^{k} \lambda_i\right)(b - a) \right)$$

Em seguida, fixe outro intervalo $[c, d]$ tal que $[a, b] \cap [c, d] = \emptyset$. Queremos mostrar que $N([a, b])$ e $N([c, d])$ são independentes.

Note que:

$$N([a, b]) = F\left(N^{(1)}([a, b]), \dots, N^{(k)}([a, b])\right)$$

$$N([c, d]) = F\left(N^{(1)}([c, d]), \dots, N^{(k)}([c, d])\right)$$

Fixe $1 \le i \le k$. É suficiente mostrar que $N^{(i)}([a, b])$ é independente de $(N^{(1)}([c, d]), \dots, N^{(k)}([c, d])$. Pela independência dos processos, precisamos verificar apenas a independência entre $N^{(i)}([a, b])$ e $N^{(i)}([c, d])$. Essas variáveis são independentes pois $N^{(i)}$ é um PPP e os intervalos são disjuntos.

---

## Decomposição de um Processo de Poisson

Seja $(N(t))_{t \ge 0}$ um $PPP(\lambda)$ e seja $(B_n)_{n \ge 1}$ uma sequência i.i.d. com distribuição $\text{Ber}(p)$, $p \in (0,1)$, independente do $PPP(N(t))_{t \ge 0}$.

Considere o processo $(N^{(1)}(t))_{t \ge 0}$ obtido da seguinte forma:

Para cada chegada $S_n$ do processo $(N(t))_{t \ge 0}$, adicionamos essa chegada ao processo $(N^{(1)}(t))_{t \ge 0}$ se $B_n = 1$. 

Além disso, defina $N^{(2)}(t) = N(t) - N^{(1)}(t), \forall t \ge 0$

Dessa forma, os processos decompõem o original no sentido de que $N(t) = N^{(1)}(t) + N^{(2)}(t)$.

**Pergunta:** Como estes processos estão distribuídos?

### Teorema 3
Os processos $(N^{(1)}(t))_{t \ge 0}$ e $(N^{(2)}(t))_{t \ge 0}$ são **independentes**. Além disso, o primeiro é um $PPP(\lambda p)$ e o segundo é um $PPP(\lambda(1-p))$.

**Prova:**
Fixe dois intervalos disjuntos $[a, b]$ e $[c, d]$. 

Precisamos mostrar que:

1. $N^{(i)}([a, b])$ e $N^{(i)}([c, d])$ são independentes para cada $i = 1, 2, \dots$ (Exercício)
2. $(N^{(1)}([a, b]), N^{(2)}([c, d]))$ ou $(N^{(1)}([c, d]), N^{(2)}([a, b]))$ são independentes. (Exercício)
3. $(N^{(1)}([a, b]), N^{(2)}([a, b]))$ são independentes.

$$\mathbb{P}(N^{(1)}([a, b]) = n, \; N^{(2)}([a, b]) = m) = \mathbb{P}\left( N([a, b]) = n + m, \; \sum_{i=1}^{n+m} B_i = n \right)$$

$$= \mathbb{P}(N([a, b]) = n + m) \cdot \mathbb{P}\left( \sum_{i=1}^{n+m} B_i = n \right)$$

$$= \left( e^{-\lambda(b - a)} \frac{(\lambda(b - a))^{n+m}}{(n + m)!} \right) \cdot \binom{n + m}{n} p^n (1 - p)^m$$

$$= e^{-\lambda(b - a)} \frac{\lambda^{n+m}(b - a)^{n+m}}{(n + m)!} \cdot \frac{(n + m)!}{n! \, m!} p^n (1 - p)^m$$

$$= \left( e^{-\lambda p (b - a)} \frac{(\lambda p (b - a))^n}{n!} \right) \cdot \left( \frac{(\lambda (1 - p) (b - a))^m}{m!} e^{-\lambda (1 - p) (b - a)} \right)$$
