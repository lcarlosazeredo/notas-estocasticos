# Aula 26

**Data:** 20/05/2026

## Processos Pontuais de Poisson (PPP)

$Def.:$ Seja $(N(t))_{t \ge 0}$ um processo de contagem. Esse processo é de **Poisson** de taxa $\lambda > 0$, se:

1. $N([a,b]) \sim \text{Poi}(\lambda(b-a)), \quad \forall a, b \in [0, \infty), \;\; a < b$
2. $\forall a_1, a_2, a_3, \dots, a_k, b_1, \dots, b_k \in [0, \infty)$ t.q. $a_i < b_i < a_i+1, i = 1, \dots, k-1$. As variáveis $N([a_i, b_i])$ são independentes.

> $\hookrightarrow$ Note que a condição 1 nos diz que $N([a+t, b+t]) \sim N([a,b]), \; \forall t \ge 0$

---

## Validação por Construção
Na construção vista na aula passada:

$$N([a, b] \cap A_i) \sim \text{Poi}(\lambda |[a, b] \cap A_i|)$$

Para cada $i = 1, 2, \dots$

Usando a propriedade da soma de variáveis de Poisson independentes:

$$N([a, b]) = N([a, b] \cap A_{ia}) + \dots + N([a, b] \cap A_{ib})$$

* Onde $ia$ é o índice $i$ tal que $a \in A_{i_a}$.
* Onde $ib$ é o índice $i$ tal que $b \in A_{i_b}$.

Como $N([a, b] \cap A_i) \sim \text{Poi}(\lambda |[a, b] \cap A_i|)$, temos pelo resultado final que:

$$N([a, b]) \sim \text{Poi}(\lambda(b - a))$$

A condição 2 segue da construção.

---

## Tempos Entre Chegadas (Instantes entre Saltos)

Defina $T_1 = \mathcal{S_1}$ e $T_n = \mathcal{S_n} - \mathcal{S_{}n-1}$, para $n \ge 1$, como os **instantes entre saltos** (ou tempos entre chegadas) do processo.

**Perguntas:** Qual é a distribuição de $T_n$? São independentes?

Para $T_1$:

$$P(T_1 > t) = P(N(t) = 0) = P(N((0, t]) = 0) = e^{-\lambda t}, \quad \forall t > 0$$

Logo, $T_1 \sim \text{Exp}(\lambda)$

Na realidade, podemos provar que: $T_n \sim \text{Exp}(\lambda), \quad \forall n \ge 1$

Além disso, $T_1, T_2, T_3, \dots$ **são independentes**. Em particular, $\mathbb{E}[T_n] = \frac{1}{\lambda}$

---

Pode-se mostrar que o processo definido por:

$$N(t) = \max\{n : T_1 + T_2 + \dots + T_n \le t\}, \quad t \ge 0$$

Define um processo de contagem de Poisson de taxa $\lambda > 0$.

---

## Propriedade Forte de Markov

Seja $(N(t))_{t \ge 0}$ um processo de contagem de $PPP(\lambda)$. 

Defina,

$$N_{(t)}^{(k)} = N((\mathcal{S_k}, \mathcal{S_{k+t}}]), t \ge 0$$

Então $(N_{(t)}^{(k)})_{t \ge 0}$ define um processo de contagem de $PPP(\lambda)$, que é independente de $(N_{(s)})_{s \le \mathcal{S_k}}$

---

Fixado $h > 0$

Defina:

$$\tilde{N}(t) = N((h, h + t]), \quad t \ge 0$$

**Perguntas:**

1. $(\tilde{N}(t))_{t \ge 0} \in PPP(\lambda)$?
2. $(\tilde{N}(t))_{t \ge 0}$ é independente de $(N(t))_{t \le h}$?

---

Analisando um intervalo genérico $[a, b]$:

$$\tilde{N}([a, b]) = \tilde{N}(b) - \tilde{N}(a) = N((h, h + b]) - N((h, h + a]) = N((h + a, h + b])$$

$$= N((h + a, h + b]) \sim \text{Poi}(\lambda(b - a))$$

---

Analisando a independência:

$t_1 < t_2 < \dots < t_k, \quad s_1 < s_2< \dots < s_l \le h$

$h < h + t_0 < h + t_1 < \dots < h + t_k$

$$\mathbb{P}\left( \tilde{N}(t_1) = n_1, \tilde{N}(t_2) = n_2, \dots, \tilde{N}(t_k) = n_k, N(s_1) = m_1, \dots, N(s_l) = m_l \right)$$

$$= \mathbb{P}\left( \bigcap_{j=0}^{k-1} \{N((h+t_j, h+t_{j+1}])) = n_{j+1} - n_j\}, \bigcap_{j=0}^{l-1} \{N((s_j, s_{j+1}])) = m_{j+1} - m_j\} \right)$$

$$= \mathbb{P}\left( \bigcap_{j=0}^{k-1} \{N((h+t_j, h+t_{j+1}])) = n_{j+1} - n_j\} \right) \cdot \mathbb{P}\left( \bigcap_{j=0}^{l-1} \{N((s_j, s_{j+1}])) = m_{j+1} - m_j\} \right)$$

$$= \left( \prod_{j=0}^{k-1} \frac{e^{-\lambda(t_{j+1}-t_j)} [\lambda(t_{j+1}-t_j)]^{n_{j+1}-n_j}}{(n_{j+1}-n_j)!} \right) \cdot \left( \prod_{j=0}^{l-1} \frac{e^{-\lambda(s_{j+1}-s_j)} [\lambda(s_{j+1}-s_j)]^{m_{j+1}-m_j}}{(m_{j+1}-m_j)!} \right)$$




























