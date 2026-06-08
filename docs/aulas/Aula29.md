# Aula 29

**Data:** 27/05/2026

## Filas M/G/$\infty$

Consideramos um processo $(N_t)_{t \ge 0} \sim \text{PPP}(\lambda)$ que descreve a chegada dos clientes. 

Cada cliente tem um tempo de atendimento cuja FDA é $F$, independente de todo o resto.

Para cada $t \ge 0$, definimos:

* $Y_t$: # de clientes atendidos no tempo $t$.
* $X_t$: # de clientes em atendimento no tempo $t$.

Temos, para todo $t \ge 0$:

$$N_t = X_t + Y_t$$

---

### Proposição
$X_t$ e $Y_t$ são independentes. Além disso,

$$X_t \sim \text{Poi}\left(\lambda \int_{0}^{t} (1 - F(u)) \, du\right)$$

$$Y_t \sim \text{Poi}\left(\lambda \int_{0}^{t} F(u) \, du\right)$$

**Prova:**
Seja $U_j$ a $j$-ésima variável uniforme que indica o tempo de chegada do cliente, e $W_j$ o tempo de atendimento do cliente que chegou no tempo $U_j$.

Este cliente estará em atendimento no tempo $t$ com probabilidade $\mathbb{P}(W_j > t - U_j) = \mathbb{P}(W_1 > t - U_1)$. Sabendo disso:

$$\mathbb{P}(W_1 > t - U_1) = \int_{0}^{t} \frac{1}{t} \mathbb{P}(W_1 > t - u) \, du = \frac{1}{t} \int_{0}^{t} (1 - F(t - u)) \, du$$

Fazendo a mudança de variáveis $v = t - u \Rightarrow du = -dv$:

$$= \frac{1}{t} \int_{t}^{0} (1 - F(v)) \, (-dv) = \frac{1}{t} \int_{0}^{t} (1 - F(u)) \, du = p$$

Dessa forma, condicionado ao número total de chegadas $N_t = n$, a distribuição de clientes em atendimento segue uma Binomial:

$$X_t \mid N_t = n \sim \text{Bin}\left(n, \frac{1}{t} \int_{0}^{t} (1 - F(u)) \, du\right)$$

Como consequência:

$$\mathbb{P}(X_t = x, Y_t = y) = \mathbb{P}(X_t = x, Y_t = y, N_t = x + y)$$

$$ = \mathbb{P}(N_t = x + y) \cdot \mathbb{P}(X_t = x, Y_t = y \mid N_t = x + y)$$

$$= e^{-\lambda t} \frac{(\lambda t)^{x+y}}{(x+y)!} \cdot \mathbb{P}(X_t = x \mid N_t = x + y)$$

$$= e^{-\lambda t} \frac{(\lambda t)^{x+y}}{(x+y)!} \cdot \binom{x+y}{x} p^x (1-p)^y$$

$$= e^{-\lambda t} \frac{(\lambda t)^{x+y}}{(x+y)!} \cdot \frac{(x+y)!}{x! \, y!} p^x (1-p)^y$$

$$= e^{-\lambda t p} \frac{(\lambda t p)^x}{x!} \cdot e^{-\lambda t (1-p)} \frac{(\lambda t (1-p))^y}{y!}$$

Logo, $X_t$ e $Y_t$ são independentes e:

$$X_t \sim \text{Poi}(\lambda t p)$$

$$Y_t \sim \text{Poi}(\lambda t (1-p))$$

Para concluir, observe que:

$$\lambda t p = \lambda \int_{0}^{t} (1 - F(u)) \, du$$

$$\lambda t (1-p) = \lambda \int_{0}^{t} F(u) \, du$$

---

## Descrição Alternativa de um PPP$(\lambda)$

Seja $(N_t)_{t \ge 0}$ um $\text{PPP}(\lambda)$.

* **Afirmação 1 (AF.1):** $\mathbb{P}(N_t \ge 2) = o(t) \iff \lim_{t \to 0} \frac{\mathbb{P}(N_t \ge 2)}{t} = 0$
* **Afirmação 2 (AF.2):** $\mathbb{P}(N_t = 1) = \lambda t + o(t) \iff \lim_{t \to 0} \frac{\mathbb{P}(N_t = 1)}{t} = \lambda$

### Prova da AF.2:

$$\mathbb{P}(N_t = 1) = e^{-\lambda t} \lambda t = \lambda t + \underbrace{\lambda t (e^{-\lambda t} - 1)}_{o(t)}$$

Como,

$$\lim_{t \to 0} \frac{\lambda t (e^{-\lambda t} - 1)}{t} = \lim_{t \to 0} \lambda (e^{-\lambda t} - 1) = 0$$

### Prova da AF.1:

$$\mathbb{P}(N_t = 0) = e^{-\lambda t} = 1 - \lambda t + \sum_{n=2}^{\infty} \frac{(-1)^n (\lambda t)^n}{n!}$$

Temos que:

$$\left| \sum_{n=2}^{\infty} \frac{(-1)^n (\lambda t)^n}{n!} \right| \le \sum_{n=2}^{\infty} \frac{\lambda^n t^n}{n!} = t \left[ \frac{\lambda^2 t}{2!} + \frac{\lambda^3 t^2}{3!} + \frac{\lambda^4 t^3}{4!} + \dots \right]$$

$$= t \cdot \frac{\lambda^2 t}{2} \left[ 1 + \frac{t\lambda}{3} + \frac{(t\lambda)^2}{4 \cdot 3} + \frac{(t\lambda)^3}{5 \cdot 4 \cdot 3} + \dots \right]$$

$$\le \frac{t^2 \lambda^2}{2} \left[ 1 + \frac{t\lambda}{3} + \left(\frac{t\lambda}{3}\right)^2 + \left(\frac{t\lambda}{3}\right)^3 + \dots \right] = \frac{t^2 \lambda^2}{2} \sum_{n=0}^{\infty} \left(\frac{t\lambda}{3}\right)^n$$

$$= \frac{t^2 \lambda^2}{2} \cdot \frac{1}{1 - \frac{t\lambda}{3}}, \quad \text{para } \frac{t\lambda}{3} < 1 \iff t < \frac{3}{\lambda}$$

Logo, avaliando o complementar para $\mathbb{P}(N_t \ge 2)$:

$$\mathbb{P}(N_t \ge 2) = 1 - (\mathbb{P}(N_t = 0) + \mathbb{P}(N_t = 1))$$

$$\mathbb{P}(N_t \ge 2) = 1 - (1 - \lambda t + o(t) + \lambda t + o(t)) = o(t)$$

---

## Cadeias de Markov em Tempo Contínuo

Seja $(X_t)_{t \ge 0}$ um processo estocástico em tempo contínuo e tomando valores em um conjunto $\mathcal{X}$ enumerável.

$Def.:$ $(X_t)_{t \ge 0}$ é uma Cadeia de Markov se:

$$\mathbb{P}(X_{t_{n+1}} = x_{n+1} \mid X_{t_n} = x_n, \dots, X_{t_1} = x_1, X_{t_0} = x_0) = \mathbb{P}(X_{t_{n+1}} = x_{n+1} \mid X_{t_n} = x_n)$$

Para quaisquer $0 =: t_0 < t_1 < \dots < t_n < t_{n+1}$ e quaisquer $x_0, x_1, \dots, x_{n+1} \in \mathcal{X}$.

Se, além disso,

$$\mathbb{P}(X_{t+s} = y \mid X_s = x) = \mathbb{P}(X_t = y \mid X_0 = x)$$

Dizemos que a Cadeia de Markov é **Tempo Homogêneo**. Neste caso, escreveremos:

$$P_t(x, y) = \mathbb{P}(X_t = y \mid X_0 = x)$$

Sendo $P_t = (P_t(x, y))_{x, y \in \mathcal{X}}$ a matriz de transição.

---

### Propriedades

1. $P_t$ é uma matriz estocástica para todo $t \ge 0$, com $P_0 = I$ (matriz identidade).
2. Valem as **Equações de Chapman-Kolmogorov**:

$$P_{t+s} = P_t P_s = P_s P_t, \quad \forall s, t \ge 0$$

### Distribuições Conjuntas

As distribuições conjuntas ficam determinadas para quaisquer $n \ge 1$ e $0 =: t_0 < t_1 < \dots < t_n$:

$$\mathbb{P}(X_{t_1} = x_1, X_{t_2} = x_2, \dots, X_{t_n} = x_n) = \sum_{x_0 \in \mathcal{X}} \mathbb{P}(X_0 = x_0) \prod_{j=0}^{n-1} P_{t_{j+1} - t_j}(x_j, x_{j+1})$$

Usaremos a notação $\mathbb{P}_\pi$ para indicar que $X_0 \sim \pi$. Em particular:

$$\mathbb{P}_\pi(X_t = y) = \sum_{x \in \mathcal{X}} \pi(x) P_t(x, y) = (\pi P_t)(y)$$

Escrevemos $\pi_t = \pi P_t$. Quando $\pi = \delta_x$, escrevemos $\mathbb{P}_x$ ao invés de $\mathbb{P}_{\delta_x}$.

---

### Exemplos

#### 1. Processo de Poisson
Aqui, o espaço de estados é $\mathcal{X} = \mathbb{N}$.

$$P_t(x, y) = \mathbb{P}(N_{t+s} = y \mid N_s = x) = \mathbb{P}(N_{t+s} = y \mid N_{s} = x)$$

$$ = \mathbb{P}(N((s, t+s]) = y - x) = e^{-\lambda t} \frac{(\lambda t)^{y-x}}{(y-x)!}, \quad \text{se } y \ge x$$

$$P_t(x, y) = 0, \quad \text{se } y < x$$