# Aula 30

**Data:** 29/05/2026

## Revisão:

Considere um processo estocástico $(X_t)_{t \ge 0}$ assumindo valores em um espaço de estados $\mathcal{X}$ enumerável tal que:

$$\mathbb{P}(X_{t_{n+1}} = x_{n+1} \mid X_{t_n} = x_n, \dots, X_{t_1} = x_1, X_{t_0} = x_0) = \mathbb{P}(X_{t_{n+1}} = x_{n+1} \mid X_{t_n} = x_n)$$

Para quaisquer $0 = t_0 < t_1 < t_2 < \dots < t_n < t_{n+1}$.

---

Tempo Homogêneo

A cadeia é dita **tempo homogêneo** se:

$$\mathbb{P}(X_{t+s} = y \mid X_s = x) = \mathbb{P}(X_t = y \mid X_0 = x) = P_t(x, y), \quad \forall t, s \ge 0, \;\; \forall x, y \in \mathcal{X}$$

---

## Exemplos

### 1. Processo de Poisson $(N_t)_{t \ge 0}$
Como $N_t = N_s + N((s, t])$ para todo $t > s$, temos que:

$$\mathbb{P}(N_{t_3} = z \mid N_{t_2} = y, N_{t_1} = x, N_{t_0} = x_0) = \mathbb{P}(N_{t_3} = z \mid N_{t_1} = x, N((t_1, t_2]) = y - x)$$

$$= \mathbb{P}(N((t_2, t_3]) = z - y \mid N_{t_1} = x, N((t_1, t_2]) = y - x)$$

$$= \mathbb{P}(N((t_2, t_3]) = z - y) = e^{-\lambda(t_3 - t_2)} \frac{(\lambda(t_3 - t_2))^{z - y}}{(z - y)!}$$

De modo geral, para $t_3 > t_2$:

$$\mathbb{P}(N_{t_3} = z \mid N_{t_2} = y) = \mathbb{P}(N((t_2, t_3]) = z - y \mid N_{t_2} = y)$$

$$= \mathbb{P}(N((t_2, t_3]) = z - y) = \mathbb{P}(N_{t_3 - t_2} = z - y)$$

---

### 2. Processo de Poisson Composto
Definimos o processo por:

$$X_t = X_0 + \sum_{i=1}^{N_t} Y_i, \quad t \ge 0$$

Onde $(N_t)_{t \ge 0} \sim \text{PPP}(\lambda)$ e $(Y_i)_{i \ge 1}$ é uma sequência de variáveis aleatórias i.i.d., independentes do processo de Poisson, com $X_0$ v.a. independente de todo o resto.

Queremos calcular:

$$\mathbb{P}(X_{t_{n+1}} = x_{n+1} \mid X_{t_n} = x_n, \dots, X_{t_1} = x_1, X_{t_0} = x_0)$$

Para simplificar a notação, denote $t_n = s$ e $t_{n+1} = t$. Note que:

$$X_t = X_0 + \sum_{i=1}^{N_s} Y_i + \sum_{i=N_s + 1}^{N_t} Y_i = X_s + \sum_{i=N_s + 1}^{N_s + N((s, t])} Y_i$$

Substituindo na probabilidade condicional:

$$\mathbb{P}\left(x_n + \sum_{i=N_s + 1}^{N_s + N((s, t])} Y_i = x_{n+1} \;\middle|\; X_s = x_n, \dots, X_{t_0} = x_0\right)$$

$$= \mathbb{P}\left(\sum_{i=N_s + 1}^{N_s + N((s, t])} Y_i = x_{n+1} - x_n \;\middle|\; X_s = x_n, \dots, X_{t_0} = x_0\right)$$

Usando a lei da probabilidade total condicionando no valor de $N_s = k$:

$$= \sum_{k=0}^{\infty} \mathbb{P}\left(N_s = k, \sum_{i=k + 1}^{k + N((s, t])} Y_i = x_{n+1} - x_n \;\middle|\; X_s = x_n, \dots, X_{t_0} = x_0\right)$$

$$= \sum_{k=0}^{\infty} \mathbb{P}(N_s = k \mid X_s = x_n, \dots, X_{t_0} = x_0) \cdot \mathbb{P}\left(\sum_{i=k + 1}^{k + N((s, t])} Y_i = x_{n+1} - x_n \;\middle|\; X_s = x_n, \dots, X_{t_0} = x_0, N_s = k\right)$$

Pela independência dos incrementos de Poisson e das v.a. $Y_i$:

$$\mathbb{P}\left(\sum_{i=k + 1}^{k + N((s, t])} Y_i = x_{n+1} - x_n \;\middle|\; X_s = x_n, \dots, X_{t_0} = x_0, N_s = k\right)$$

$$= \sum_{l=0}^{\infty} \mathbb{P}\left(N((s, t]) = l, \sum_{i=k + 1}^{k + l} Y_i = x_{n+1} - x_n \;\middle|\; X_s = x_n, \dots, X_0 = x_0, N_s = k\right)$$

$$= \sum_{l=0}^{\infty} \mathbb{P}(N((s, t]) = l) \cdot \mathbb{P}\left(\sum_{i=1}^{l} Y_i = x_{n+1} - x_n\right)$$

$$= \sum_{l=0}^{\infty} e^{-\lambda(t - s)} \frac{(\lambda(t - s))^l}{l!} \mathbb{P}\left(\sum_{i=1}^{l} Y_i = x_{n+1} - x_n\right)$$

Obtemos que:

$$\mathbb{P}(X_t = x_{n+1} \mid X_s = x_n, \dots, X_{t_0} = x_0) = \sum_{l=0}^{\infty} e^{-\lambda(t - s)} \frac{(\lambda(t - s))^l}{l!} \mathbb{P}\left(\sum_{i=1}^{l} Y_i = x_{n+1} - x_n\right)$$

$$= \mathbb{P}(X_{t+s} = x_{n+1} \mid X_s = x_n)$$

Verifica-se de modo similar que o Processo de Poisson Composto é uma Cadeia de Markov.

---

### 3. Troca de Sinal
Seja o processo definido por:

$$X_t = X_0 (-1)^{N_t}$$

Onde $(N_t)_{t \ge 0}$ é $\text{PPP}(\lambda)$ e $X_0 \in \{-1, +1\}$ é independente do PPP. 

> *Verificar que é um Processo de Markov.*

---

### 4. A partir de Cadeias Discretas
Consideramos um processo da forma $X_t = Z_n$, se $S_n \le t < S_{n+1}$, onde $S_n$ são os instantes de chegada de um processo de Poisson $(N_t)_{t \ge 0}$ de taxa $\lambda$ (com $S_0 = 0$).

Seja $(Z_i)_{i \ge 0}$ uma Cadeia de Markov em tempo discreto com espaço de estados $\mathcal{X}$ finito, independente dos instantes de chegada $(S_i)_{i \ge 1}$.

Denote $k = (k(x, y))_{x, y \in \mathcal{X}}$ a matriz de transição da cadeia em tempo discreto $(Z_i)_{i \ge 0}$.

**Pergunta:** Como expressar $P_t(x, y)$ a partir da matriz $k$ e do parâmetro $\lambda$?

Observe que:

$$P_t(x, y) = \mathbb{P}(X_t = y \mid X_0 = x) = \sum_{n=0}^{\infty} \mathbb{P}(N_t = n, X_t = y \mid X_0 = x)$$

$$= \sum_{n=0}^{\infty} \mathbb{P}(N_t = n \mid X_0 = x) \cdot \mathbb{P}(X_t = y \mid N_t = n, X_0 = x)$$

$$= \sum_{n=0}^{\infty} \mathbb{P}(N_t = n \mid Z_0 = x) \cdot \mathbb{P}(Z_n = y \mid N_t = n, Z_0 = x)$$

$$= \sum_{n=0}^{\infty} e^{-\lambda t} \frac{(\lambda t)^n}{n!} \cdot k^n(x, y) = \left( \sum_{n=0}^{\infty} e^{-\lambda t} \frac{(\lambda t)^n k^n}{n!} \right)(x, y)$$

$$= e^{-\lambda t} \left( \sum_{n=0}^{\infty} \frac{(\lambda t k)^n}{n!} \right)(x, y) = e^{-\lambda t} e^{\lambda t k}(x, y)$$

Dessa forma, a matriz de transição em tempo contínuo $P_t$ é dada por:

$$P_t = e^{-\lambda t} \cdot e^{\lambda t k}$$

---

### Simplificação Usando a Matriz Geradora $Q$

Lembre que:

1. $e^{A+B} = e^A \cdot e^B$ se as matrizes comutam, isto é, $AB = BA$.
2. Para $c \in \mathbb{R}$, $e^{c} I = e^{c I}$.

Usando as propriedades (1) e (2), temos:

$$P_t = e^{-\lambda t I} e^{\lambda t k} = e^{-\lambda t I + \lambda t k} = e^{\lambda t (k - I)}$$

$$P_t = e^{t Q}$$

Onde definimos a **Matriz Geradora** $Q$ como:

$$Q = \lambda (k - I)$$