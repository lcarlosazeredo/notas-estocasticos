# Aula 17

**Data:** 17/04/2026

## Revisão
* $\mathcal{T}_x^+ = \min \{ t \ge 1 : X_t = x \}$
* **$\pi$** Distribuição estacionária
* $P$ Matriz de transição irredutível
* $\mathcal{X}$ finito

### Proposição 
$\forall x \in \mathcal{X}$ fixado:

$$\pi(y) = \frac{\mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right]}{\mathbb{E}_x[\mathcal{T}_x^+]}, \quad \forall y \in \mathcal{X}$$

Em particular,

$$\pi(x) = \frac{1}{\mathbb{E}_x[\mathcal{T}_x^+]}$$

---

## Prova da Proposição
Basta verificar que $\tilde{\pi}(y) := \frac{\mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right]}{\mathbb{E}_x[\mathcal{T}_x^+]}, y \in \mathcal{X}$ satisfaz $\tilde{\pi} = \tilde{\pi}P$.

Note que:

$$\tilde{\pi}P(z) = \sum_{y \in \mathcal{X}} \tilde{\pi}(y)P(y, z)$$

$$= \frac{1}{\mathbb{E}_x[\mathcal{T}_x^+]} \sum_{y \in \mathcal{X}} \mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right] P(y, z)$$

Como

$$\mathbb{E}_x \left[ \sum_{t=0}^{\infty} \mathbb{1}_{\{\mathcal{T}_x^+ -1 \ge t\}} \mathbb{1}_{\{X_t = y\}} \right] = \sum_{t=0}^{\infty} \mathbb{E}_x \left[ \mathbb{1}_{\{\mathcal{T}_x^+ -1 \ge t, X_t = y\}} \right] = \sum_{t=0}^{\infty} \mathbb{P}_x(\mathcal{T}_x^+ -1 \ge t, X_t = y)$$

Temos:

$$\sum_{y \in \mathcal{X}} \mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right] P(y, z) = \sum_{y \in \mathcal{X}} \sum_{t=0}^{\infty} \mathbb{P}_x(\mathcal{T}_x^+ \geq t+1, X_t = y) P(y, z)$$

$$= \sum_{t=0}^{\infty} \sum_{y \in \mathcal{X}: y \neq x} \mathbb{P}_x(\mathcal{T}_x^+ \geq t+1, X_t = y) P(y, z)$$

$$= \sum_{t=0}^{\infty} \mathbb{P}_x(\mathcal{T}_x^+ \geq t+1, X_{t+1} = z) \quad (*)$$

**Se $z \neq x$:**

$$(*) = \sum_{t=0}^{\infty} \mathbb{P}_x(\mathcal{T}_x^+ \ge t+2, X_{t+1} = z) = \sum_{t=1}^{\infty} \mathbb{P}_x(\mathcal{T}_x^+ \ge t+1, X_t = z)$$

Como $\mathbb{P}_x(X_0 = z) = 0$ para $z \neq x$, podemos incluir o termo $t=0$:

$$= \sum_{t=0}^{\infty} \mathbb{P}_x(\mathcal{T}_x^+ \ge t+1, X_t = z) = \mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = z\}} \right]$$

Logo, para $z \neq x$:

$$
\begin{aligned}
\tilde{\pi} P(z) &= \sum_{y \in \mathcal{X}} \tilde{\pi}(y) P(y, z) \\
&= \frac{1}{\mathbb{E}_x[\mathcal{T}_x^+]} \mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right] = \tilde{\pi}(z)
\end{aligned}
$$

**Para** $z = x$:

$$
\begin{aligned}
(*) &= \sum_{t=0}^{\infty} \mathbb{P}_x(\mathcal{T}_x^+ = t + 1) \\
&= \sum_{t=0}^{\infty} \mathbb{E}_x[\mathbb{1}_{\{\mathcal{T}_x^+ = t + 1\}}] \\
&= \mathbb{E}_x \left[ \sum_{t=0}^{\infty} \mathbb{1}_{\{\mathcal{T}_x^+ = t + 1\}} \right] = \mathbb{E}_x[\mathbb{1}_{\{\mathcal{T}_x^+ < \infty\}}] \\
&= \mathbb{P}_x(\mathcal{T}_x^+ < \infty) = 1
\end{aligned}
$$

$$
\implies \sum_{y \in \mathcal{X}} \tilde{\pi}(y) P(y, x) = \sum_{y \in \mathcal{X}} \frac{\mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right] P(y, x)}{\mathbb{E}_x[\mathcal{T}_x^+]} = \frac{1}{\mathbb{E}_x[\mathcal{T}_x^+]} = \tilde{\pi}(x)
$$

$\implies \tilde{\pi} = \tilde{\pi} P$

---

## Reversibilidade
$Def.:$ $\pi$ vetor de probabilidade satisfaz a **Condição de Balanceamento Detalhado (CBD)** se

$$\pi(x)P(x, y) = \pi(y)P(y, x), \quad \forall x, y \in \mathcal{X}$$

$Prop.:$ Se $\pi$ satisfaz CBD, então $\pi$ é estacionária ($\pi = \pi P$).

**Prova:**

$$\pi P(y) = \sum_{x \in \mathcal{X}} \pi(x) P(x, y) = \sum_{x \in \mathcal{X}} \pi(y) P(y, x)$$

$$= \pi(y) \sum_{x \in \mathcal{X}} P(y, x) = \pi(y) \cdot 1 = \pi(y)$$

**Contra-exemplo:**
$\mathcal{X} = \{1, 2, 3\}$, $P = \begin{pmatrix} 0.4 & 0.6 & 0 \\ 0.1 & 0.7 & 0.2 \\ 0.3 & 0.2 & 0.5 \end{pmatrix}$
Suponha que $\pi$ satisfaça a CBD:

$$\pi(1)P(1, 3) = \pi(3)P(3, 1) \Rightarrow \pi(1) \cdot 0 = \pi(3) \cdot 0.3 \Rightarrow \pi(3) = 0$$

**Absurdo**, pois a única $\pi$ para esta cadeia irredutível deve ter entradas positivas.

---

**Porque esse nome?**

$\pi$ é estacionária $\iff \pi(y) = \sum_{x} \pi(x) P(x, y), \forall y \in \mathcal{X}$

$\quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad = \sum_{x} \pi(y) P(y, x)$

$\quad \quad \quad \quad \quad \quad \quad \text{(Equação de Balanceamento)}$

---

$$
\begin{aligned}
\pi(y) = \mathbb{P}_{\pi}(X_0 = y) &= \sum_{x \in \mathcal{X}} \mathbb{P}_{\pi}(X_0 = y, X_1 = x) \\
&= \sum_{x \in \mathcal{X}} \mathbb{P}_{\pi}(X_0 = y) \underbrace{\mathbb{P}_{\pi}(X_1 = x \mid X_0 = y)}_{P(y, x)}
\end{aligned}
$$

