# Aula 24

**Data:** 15/05/2026

## Convergência à Distribuição Estacionária (Caso $\mathcal{X}$ Enumerável)

### Teorema 1:
Seja $(X_t)_{t \ge 0}$ uma Cadeia de Markov irredutível, aperiódica e **recorrente positiva**. Então:

$$\lim_{t \to \infty} \mathbb{P}_{\mu}(X_t = x) = \pi(x), \quad \forall x \in \mathcal{X},$$

onde $\pi$ é a única distribuição estacionária e $\mu$ é qualquer distribuição inicial.

---

Tomando $\mu = \delta_y$, vemos que:

$$\lim_{t \to \infty} P^t(y,x) = \pi(x), \quad \forall x \in \mathcal{X}$$

Matricialmente vemos esse resultado:

$$P^t = \left[ \begin{matrix} & \vdots & \\ \dots & P^t(y,x) & \dots \\ & \vdots & \end{matrix} \right] \xrightarrow{t \to \infty} \left[ \begin{matrix} & \vdots & \\ \dots & \pi(x) & \dots \\ & \vdots & \end{matrix} \right]$$

---

Há uma versão do Teorema 1 para Cadeias **Transientes** ou **Recorrentes Nulas**.

### Teorema 2:
Seja $(X_t)_{t \ge 0}$ uma Cadeia de Markov irredutível, transiente ou recorrente nula, então:

$$\lim_{t \to \infty} \mathbb{P}_{\mu}(X_t = x) = 0, \quad \forall x \in \mathcal{X}$$

e qualquer distribuição inicial $\mu$.

---

**Prova:** (Caso transiente apenas)

Como $x$ é transiente, sabemos que $\mathbb{E}_x[N_x^+] < \infty$. 

Usando que para todo $y \in \mathcal{X}$,

$$\begin{aligned}
\mathbb{E}_y[N_x^+] &= \mathbb{E}_y\left[ N_x^+ \mathbb{1}_{\{\mathcal{T}_x^+ < \infty\}} \right] \\ \\
&= \mathbb{E}_y\left[ \left( \sum_{t=1}^{\infty} \mathbb{1}_{\{X_t = x\}} \right) \mathbb{1}_{\{\mathcal{T}_x^+ < \infty\}} \right] \\ \\
&= \mathbb{E}_y\left[ \left( \sum_{t=\mathcal{T}_x^+}^{\infty} \mathbb{1}_{\{X_t = x\}} \right) \bigcup_{s=1}^{\infty} \{ \mathcal{T}_x^+ = s \} \right] \\ \\
&= \mathbb{E}_y\left[ \left( \sum_{t=\mathcal{T}_x^+}^{\infty} \mathbb{1}_{\{X_t = x\}} \right) \left( \sum_{s=1}^{\infty} \mathbb{1}_{\{\mathcal{T}_x^+ = s\}} \right) \right] \\ \\
&= \mathbb{E}_y\left[ \sum_{s=1}^{\infty} \left( \sum_{t=\mathcal{T}_x^+}^{\infty} \mathbb{1}_{\{X_t = x\}} \right) \mathbb{1}_{\{\mathcal{T}_x^+ = s\}} \right] \\ \\
&= \mathbb{E}_y\left[ \sum_{s=1}^{\infty} \left( \sum_{h=0}^{\infty} \mathbb{1}_{\{X_{h+s} = x\}} \right) \mathbb{1}_{\{\mathcal{T}_x^+ = s\}} \right] \\ \\
&= \sum_{s=1}^{\infty} \mathbb{E}_y\left[ \mathbb{1}_{\{\mathcal{T}_x^+ = s\}} \sum_{h=0}^{\infty} \mathbb{1}_{\{X_{h+s} = x\}} \right] \\ \\
&= \sum_{s=1}^{\infty} \mathbb{P}_y(\mathcal{T}_x^+ = s) \, \mathbb{E}_y\left[ \left. \sum_{h=0}^{\infty} \mathbb{1}_{\{X_{h+s} = x\}} \,\right|\, \mathcal{T}_x^+ = s \right]
\end{aligned}$$

---

Pela **Propriedade Forte de Markov**, reiniciamos o processo a partir de $x$ no instante do tempo de parada $s$:

$$\mathbb{E}_y\left[ \left. \sum_{h=0}^{\infty} \mathbb{1}_{\{X_{h+s} = x\}} \,\right|\, \mathcal{T}_x^+ = s \right] = \mathbb{E}_x\left[ \sum_{h=0}^{\infty} \mathbb{1}_{\{X_h = 0\}} \right] = \mathbb{E}_x[N_x]$$

Substituindo de volta na somatória original:

$$\begin{aligned}
\mathbb{E}_y[N_x^+] &= \left( \sum_{s=1}^{\infty} \mathbb{P}_y(\mathcal{T}_x^+ = s) \right) \mathbb{E}_x[N_x] \\ \\
&= \mathbb{P}_y(\mathcal{T}_x^+ < \infty) \, \mathbb{E}_x[N_x] \le \mathbb{E}_x[N_x]
\end{aligned}$$

---

Logo,

$$\mathbb{E}_y[N_x^+] < \infty, \quad \text{pois } x \text{ é transiente.}$$

Como $\displaystyle\sum_{t=1}^{\infty} P^t(y,x) = \mathbb{E}_y[N_x^+] < \infty$, temos que:

$$\lim_{t \to \infty} P^t(y,x) = 0, \quad \forall y \in \mathcal{X}$$

Por fim, observe que:

$$\begin{aligned}
\mathbb{P}_{\mu}(X_t = x) &= \sum_{y \in \mathcal{X}} \mathbb{P}_{\mu}(X_0 = y) \mathbb{P}_y(X_t = x) \\ \\
&= \sum_{y \in \mathcal{X}} \mu(y) P^t(y,x) \\ \\
&\xrightarrow[t \to \infty]{} \sum_{y \in \mathcal{X}} \mu(y) \lim_{t \to \infty} P^t(y,x) = 0
\end{aligned}$$

$$\tag*{$\blacksquare$}$$

---

## Teorema Ergódico (Caso $\mathcal{X}$ Enumerável)

### Teorema 3:
Seja $(X_t)_{t \ge 0}$ uma Cadeia de Markov irredutível e recorrente positiva, com única distribuição estacionária $\pi$.

Então, para toda função $f: \mathcal{X} \to \mathbb{R}$ tal que $\displaystyle\sum_{x \in \mathcal{X}} |f(x)|\pi(x) < \infty$, e toda distribuição inicial $\mu$, temos que:

$$\mathbb{P}_{\mu}\left( \lim_{t \to \infty} \frac{1}{t+1} \sum_{s=0}^{t} f(X_s) = \mathbb{E}_{\pi}[f] \right) = 1$$

onde $\mathbb{E}_{\pi}[f] = \displaystyle\sum_{x \in \mathcal{X}} f(x)\pi(x)$

---

## Processos Pontuais de Poisson

Considere uma partição de $\mathbb{R}$ por intervalos $A_i = [l_i, l_{i+1})$, $i \in \mathbb{Z}$, com $l_i < l_{i+1}$. Chamamos $|A_i| = l_{i+1} - l_i$ o comprimento do intervalo $A_i$.

$$\begin{cases}
\displaystyle\bigcup_{i \in \mathbb{Z}} A_i = \mathbb{R} \\ \\
A_i \cap A_j = \emptyset, \quad \forall i \neq j
\end{cases}$$

---

Considere $(Y_i)_{i \in \mathbb{Z}}$ variáveis aleatórias independentes tais que $Y_i \sim \text{Poi}(\lambda |A_i|)$:

$$\mathbb{P}(Y_i = k) = e^{-\lambda |A_i|} \frac{(\lambda |A_i|)^k}{k!}, \quad k \ge 0$$

Considere, para cada $i \in \mathbb{Z}$, uma família $\{U_{i,j} : j = 1, 2, 3, \dots \}$ de variáveis i.i.d, uniformemente distribuídas em $A_i$:

$$\mathbb{P}(U_{i,j} \in A) = \frac{|A \cap A_i|}{|A_i|}, \quad \text{A é um intervalo de $\mathbb{R}$}$$

---

Seja $\mathcal{S}$ o conjunto aleatório definido por:

$$\mathcal{S} = \bigcup_{i \in \mathbb{Z}} \mathcal{S_i}, \quad \text{onde } \mathcal{S_i} = \begin{cases} \{U_{i,j} : j = 1, \dots, Y_i\} & \text{se } Y_i \ge 1 \\ \emptyset & \text{se } Y_i = 0 \end{cases}$$

> **Em palavras:** Coloque $Y_i$ pontos uniformemente distribuídos em cada intervalo $A_i$, de maneira independente.

---

Finalmente, ordene os pontos em $\mathcal{S}$ de forma crescente:

* $\mathcal{S_1} = \min\{s > 0 : s \in \mathcal{S}\}$
* $\mathcal{S_n} = \min\{s > S_{n-1} : s \in \mathcal{S}\}$, para $n \ge 2$
* $\mathcal{S_0} = \max\{s < S_1 : s \in \mathcal{S}\}$
* $\mathcal{S_{n-1}} = \max\{s < S_{-n+1} : s \in \mathcal{S}\}$, para $n \le -1$


