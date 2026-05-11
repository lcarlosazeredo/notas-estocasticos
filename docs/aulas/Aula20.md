# Aula 20

**Data:** 04/05/2026

## Revisão: Algoritmo de Metropolis-Hastings
Seja $Q = (Q(x, y))_{x, y \in \mathcal{X}}$ uma matriz de transição de uma cadeia de Markov sugerida. Construímos uma nova matriz estocástica $P = (P(x, y))_{x, y}$ dada por:

$$P(x, y) = \alpha(x, y)Q(x, y), \quad x \neq y$$

$$P(x, x) = Q(x, x) + \sum_{y \neq x} (1 - \alpha(x, y))Q(x, y)$$

---

## Dinâmica de Glauber / Amostrador de Gibbs
Considere o espaço de estados $\mathcal{X} = S^V$, onde:

* $V$ é o conjunto finito de vértices de um grafo $G = (V, E)$.
* $S$ é um conjunto finito de estados para cada vértice.
* $\mathcal{X} = \{x = (x_v)_{v \in V} : x_v \in S, \forall v \in V\}$.

**Exemplo:** $\mathcal{X} = \{-1, 1\}^V = \{x = (x_v)_{v \in V} : x_v \in \{-1, 1\} \}$

### Distribuições Condicionais Completas
Seja $\pi$ uma medida de probabilidade em $\mathcal{X}$ cujas distribuições condicionais completas são conhecidas:

$$\pi^{v, x}(y) = \begin{cases} \frac{\pi(y)}{\pi(\mathcal{X}(v, x))} & \text{se } y \in \mathcal{X}(v, x) \\ 0 & \text{se } y \notin \mathcal{X}(v, x) \end{cases}$$

Onde $\mathcal{X}(v, x) = \{y \in \mathcal{X} : y_u = x_u, \forall u \neq v\}$

Em outras palavras, $\pi^{v, x}$ é a distribuição $\pi$ condicionada ao conjunto $\mathcal{X}(v, x)$.

---

### Funcionamento da Dinâmica de Glauber
Suponha que a cadeia esteja no estado $x$. E aplique a seguinte regra para escolher uma novo vértice $y$:

1. Escolha um vértice em $V$ uniformemente ao acaso.
2. Se $v$ foi o vértice escolhido, amostre da distribuição $\pi^{v, x}$ para obter a nova configuração $y$.

A matriz de transição $P$ associada a essa dinâmica é dada por:

$$P(x, y) = \frac{1}{|V|} \sum_{v \in V} \pi^{v, x}(y)$$

De forma simplificada:

* $P(x, y) = \frac{1}{|V|} \pi^{v^*, x}(y)$ se $y$ e $x$ coincidem a menos do vértice $v^*$.

* $P(x, y) = 0$ se $y$ e $x$ são distintas em mais de um vértice.

### Reversibilidade
Observe também que para $x, y$ que são distintos em no máximo um vértice, digamos $v^*$, temos que:

$$\pi(x) P(x, y) = \pi(x) \frac{1}{|V|} \left( \frac{\pi(y)}{\pi(\mathcal{X}(v^*, x))} \right)$$

$$\pi(y) P(y, x) = \pi(y) \frac{1}{|V|} \left( \frac{\pi(x)}{\pi(\mathcal{X}(v^*, y))} \right)$$

Como $\mathcal{X}(v^*, x) = \mathcal{X}(v^*, y)$, segue que $\pi(\mathcal{X}(v^*, x)) = \pi(\mathcal{X}(v^*, y))$, logo:

$$\pi(x) P(x, y) = \pi(y) P(y, x)$$