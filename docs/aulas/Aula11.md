# Aula 11

**Data:** 01/04/2026

## Ruína do Jogador
Consideramos um passeio aleatório no espaço de estados $\{0, 1, \dots, N\}$ com probabilidade $p \in [0, 1]$.

* **$\mathcal{T}_{\{0, N\}} = \min \{t \ge 0 : X_t \in \{0, N\}\}$:** Tempo de absorção.
* **$E_k[\mathcal{T}_{\{0, N\}}] = ?$:** Esperança do tempo de absorção partindo de $k$.
* **$\mathcal{T}_x = \min \{t \ge 0 : X_t = x\}$:** Tempo de visita ao estado $x \in \{0, \dots, N\}$.
* **$\mathcal{T}_{\{0, N\}} = \min \{\mathcal{T}_0, \mathcal{T}_N\}$**.
* **$P_k(\mathcal{T}_N < \mathcal{T}_0) = ?$:** Probabilidade de atingir $N$ antes de $0$ partindo de $k$.

---

## Tempo de Parada
$Def.:$ Seja $\mathcal{T}$ uma V.A. tomando valores em $\mathbb{N} \cup \{0, \infty\}$.
$\mathcal{T}$ é um **tempo de parada** se, para todo $t \ge 0$, o evento $\{\mathcal{T} = t\}$ só depende de $X_0, X_1, \dots, X_t$.

### Exemplos:
1.  **Ruína do Jogador:** $\mathcal{T}_0 = \min \{t \ge 0 : X_t = 0\}$ e $\mathcal{T}_N = \min \{t \ge 0 : X_t = N\}$.
    * $\{\mathcal{T}
_0 = t\} = \{X_0 \neq 0, X_1 \neq 0, X_2 \neq 0, \dots, X_t = 0\}$, $\forall t \ge 1$.
    * $\{\mathcal{T}
_0 = 0\} = \{X_0 = 0\}$.
2.  $\mathcal{T}_{\{0, N\}} = \min \{t : X_t \in \{0, N\}\}$ é tempo de parada, pois:
    * $\{\mathcal{T}
_{\{0, N\}} = t\} = \{X_0 \notin \{0, N\}, X_1 \notin \{0, N\}, \dots, X_{t-1} \notin \{0, N\}, X_t \in \{0, N\}\}$, $\forall t \ge 1$.
    * $\{\mathcal{T}
_{\{0, N\}} = 0\} = \{X_0 \in \{0, N\}\}$.
3.  **Mais Geralmente:** Para $A \subseteq \mathcal{X}$, $\mathcal{T}_A = \min \{t \ge 0 : X_t \in A\}$ também é tempo de parada.
4.  Além disso, $\mathcal{T}_A^+ = \min \{t \ge 1 : X_t \in A\}$ também é tempo de parada.

---

## Propriedade Forte de Markov
$Def.:$ Para todo tempo de parada $\mathcal{T}$:

$$P(X_{\mathcal{T}+s} = y \mid A, \mathcal{T} = t, X_{\mathcal{T}} = x) = P_x(X_s = y)$$

Onde $A$ é um evento tal que $A \cap \{\mathcal{T} = t\}$ depende só de $X_0, \dots, X_t$. Válido para todo $s \ge 0, t \ge 1, x, y \in \mathcal{X}$.

**Proposição:** Se $(X_t)_{t \ge 0}$ é uma Cadeia de Markov, então $(X_t)_{t \ge 0}$ satisfaz a propriedade forte.

**Prova:**
Escreva $A \cap \{\mathcal{T} = t\} = \{X_0 \in B_0, X_1 \in B_1, \dots, X_t \in B_t\}$ para $B_0, B_1, \dots, B_t$ subconjuntos de $\mathcal{X}$.

E note que:

$$P(X_{t+s} = y \mid X_0 \in B_0, \dots, X_{t-1} \in B_{t-1}, X_t = x) =$$

$$= P(X_{t+s} = y \mid X_t = x) = P_x(X_s = y)$$

---

Para analisar a **Ruína do Jogador**, precisaremos da seguinte forma da propriedade forte:

$$P(X_{\mathcal{T}+1} = x_1, X_{\mathcal{T}+2} = x_2, \dots, X_{\mathcal{T}+s} = x_s \mid A, \mathcal{T} = t, X_{\mathcal{T}} = x_0) =$$

$$= P_{x_0}(X_1 = x_1, X_2 = x_2, \dots, X_s = x_s)$$

$\forall s \ge 1, \forall t \ge 1, x_0, \dots, x_n \in \mathcal{X}$, $\mathcal{T}$ tempo de parada e evento $A$ tal que $A \cap \{\mathcal{T} = t\}$ depende somente de $X_0, \dots, X_t$.

---

## Aplicação à Ruína do Jogador

Defina $p_k = \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0)$, $0 \le k \le N$.

* $p_0 = 0$
* $p_N = 1$

Vamos analisar para $1 \le k \le N-1$:

$$p_k = \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0, X_1 = k-1) + \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0, X_1 = k+1)$$

$$= \mathbb{P}_k(X_1 = k-1)\mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 \mid X_1 = k-1) + \mathbb{P}_k(X_1 = k+1)\mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 \mid X_1 = k+1)$$

$$= (1-p)p_{k-1} + p p_{k+1}$$

pois:

* $p_{k-1} = \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 \mid X_1 = k-1)$
* $p_{k+1} = \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 \mid X_1 = k+1)$

---

### Análise $\mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 \mid X_1 = k-1)$

Para $2 \le k \le N-2$:

$$\mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 \mid X_1 = k-1)$$

$$= \mathbb{P}_k\left( \bigcup_{t=0}^{\infty} \{\mathcal{T}_N = t, \mathcal{T}_0 > t\} \mid X_1 = k-1 \right)$$

$$= \sum_{t=0}^{\infty} \mathbb{P}_k(\mathcal{T}_N = t, \mathcal{T}_0 > t \mid X_1 = k-1)$$

$$= \sum_{t=2}^{\infty} \mathbb{P}_k(X_0 \neq \{0, N\}, X_1 \neq \{0, N\}, \dots, X_{t-1} \neq \{0, N\}, X_t = N \mid X_1 = k-1)$$ 

$$= \sum_{t=2}^{\infty} \mathbb{P}_k(X_2 \neq \{0, N\}, \dots, X_{t-1} \neq \{0, N\}, X_t = N \mid X_1 = k-1)$$ 

$$= \sum_{t=2}^{\infty} \mathbb{P}_k(X_2 \neq \{0, N\}, \dots, X_{t-1} \neq \{0, N\}, X_t = N \mid \mathcal{T} = 1, X_{\mathcal{T}} = k-1)$$ 

Onde $\mathcal{T} = \mathcal{T}_{\{k-1\}} := \min \{t \ge 0 : X_t = k-1\}$.

$$= \sum_{t=2}^{\infty} \mathbb{P}_k(X_{\mathcal{T}+1} \neq \{0, N\}, \dots, X_{\mathcal{T}+(t-2)} \neq \{0, N\}, X_{\mathcal{T}+(t-1)} = N \mid \mathcal{T} = 1, X_{\mathcal{T}} = k-1)$$ 

$$= \sum_{t'=1}^{\infty} \mathbb{P}_k(X_{\mathcal{T}+1} \neq \{0, N\}, \dots, X_{\mathcal{T}+t'-1} \neq \{0, N\}, X_{\mathcal{T}+t'} = N \mid \mathcal{T} = 1, X_{\mathcal{T}} = k-1)$$ 

$$= \sum_{t=1}^{\infty} \mathbb{P}_{k-1}(X_1 \neq \{0, N\}, \dots, X_{t-1} \neq \{0, N\}, X_{t} = N)$$ 

$$= \sum_{t=1}^{\infty} \mathbb{P}_{k-1}(X_0 \neq \{0, N\}, \dots, X_{t-1} \neq \{0, N\}, X_{t} = N)$$ 

$$= \sum_{t=1}^{\infty} \mathbb{P}_{k-1}(\mathcal{T}_N = t, \mathcal{T}_0 > t)$$ 

$$= \sum_{t=0}^{\infty} \mathbb{P}_{k-1}(\mathcal{T}_N = t, \mathcal{T}_0 > t) = \mathbb{P}_{k-1}\left( \bigcup_{t=0}^{\infty} \{\mathcal{T}_N = t, \mathcal{T}_0 > t\} \right)$$ 

$$= \mathbb{P}_{k-1}(\mathcal{T}_N < \mathcal{T}_0) = p_{k-1}$$ 