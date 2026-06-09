# Aula 32

**Data:** 03/06/2026

## Construção de uma Cadeia de Markov em Tempo Contínuo 

Dada uma matriz $Q = (Q(x,y))_{x,y \in \mathcal{X}}$ uma matriz tal que:

1. $Q(x,y) \ge 0, \quad \forall x \neq y$ (taxa de sair de $x$ para $y$)
2. $\lambda(x) := \sum_{y \neq x} Q(x,y) = -Q(x,x)$ (taxa de saída de $x$), com $\lambda(x) < \infty$ para todo $x \in \mathcal{X}$

Se $\lambda(x) > 0$, definimos a matriz de transição da **Cadeia Imersa** por:

$$\tilde{P}(x,y) = \begin{cases} \frac{Q(x,y)}{\lambda(x)}, & \text{se } y \neq x \\ 0, & \text{se } y = x \end{cases}$$

Note que $\tilde{P} = (\tilde{P}(x,y))_{x,y \in \mathcal{X}}$ é uma matriz estocástica.

---

### Ideia da Construção:

Dado que $X_t = x$, o processo deve aguardar um tempo aleatório com distribuição $Exp(\lambda(x))$ para realizar um salto, e escolhe um novo estado com probabilidade $\tilde{P}(x,y)$.

Para formalizar esta construção, sejam:

1. $(\mathcal{T_n})_{n \ge 1}$ uma sequência de variáveis aleatórias i.i.d. com distribuição $Exp(1)$.
2. $(\tilde{Z}_n)_{n \ge 0}$ uma Cadeia de Markov em tempo discreto com matriz de transição $\tilde{P}$, independente de $(\mathcal{T_n})_{n \ge 1}$.

### Construção Rigorosa:

* **Inicialização:** $X_0 = \tilde{Z}_0$.
* A cadeia fica então um tempo $\tilde{\mathcal{T}}_1 = \frac{\mathcal{T_1}}{\lambda(\tilde{Z}_0)}$ no estado $\tilde{Z}_0$ e salta para $\tilde{Z}_1$.
* Em seguida, a cadeia fica um tempo $\tilde{\mathcal{T}}_2 = \frac{\mathcal{T_2}}{\lambda(\tilde{Z}_1)}$ no estado $\tilde{Z}_1$ e salta para $\tilde{Z}_2$.
* Procede-se desta forma para definir o restante do processo.



Isto é, definindo o instante do $n$-ésimo salto como:

$$\tilde{S}_n = \tilde{\mathcal{T}}_1 + \dots + \tilde{\mathcal{T}_n}$$

Colocamos:

$$X_t = \begin{cases} \tilde{Z}_0, & \text{se } 0 \le t < \tilde{S}_1 \\ \tilde{Z}_n, & \text{se } \tilde{S}_n \le t < \tilde{S}_{n+1}, \quad \text{para } n \ge 1 \end{cases}$$

Esta construção está bem definida desde que:

$$\lim_{n \to \infty} \tilde{S}_n = \infty \quad \text{com prob. 1}$$ 

---

### Verificação das Taxas de Transição

Será que $P_t = e^{tQ}$?

Será que $\lim_{t \to 0} \frac{P_t(x,y)}{t} = Q(x,y)$ para $x \neq y$, e $\lim_{t \to 0} \frac{P_t(x,x) - I}{t} = - \lambda(x)$?

Fixe $x \neq y$:

$$P_t(x,y) = \mathbb{P}(X_t = y \mid X_0 = x)$$

$$= \mathbb{P}(\tilde{S}_1 \le t < \tilde{S}_2, X_t = y \mid X_0 = x) + \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)$$

$$= \mathbb{P}\left(\frac{\mathcal{T_1}}{\lambda(x)} \le t < \frac{\mathcal{T_1}}{\lambda(x)} + \frac{\mathcal{T_2}}{\lambda(y)}, \tilde{Z}_1 = y \;\middle|\; \tilde{Z}_0 = x\right) + \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)$$

$$= \tilde{P}(x,y) \int_{0}^{t} \lambda(x)e^{-\lambda(x)s} \mathbb{P}\left(\frac{\mathcal{T_2}}{\lambda(y)} \ge t - s\right) ds + \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)$$

$$= \tilde{P}(x,y) \int_{0}^{t} \lambda(x)e^{-\lambda(x)s} e^{-\lambda(y)(t - s)} ds + \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)$$

$$= \tilde{P}(x,y) \lambda(x) e^{-\lambda(y)t} \int_{0}^{t} e^{-(\lambda(x) - \lambda(y))s} ds + \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)$$

$$= \frac{\tilde{P}(x,y)\lambda(x)e^{-\lambda(y)t}}{\lambda(x) - \lambda(y)} \left( 1 - e^{-(\lambda(x) - \lambda(y))t} \right) + \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)$$

$$= \frac{\tilde{P}(x,y)\lambda(x)e^{-\lambda(y)t}}{\lambda(x) - \lambda(y)} \Big[ (\lambda(x) - \lambda(y))t + o(t) \Big] + \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)$$

$$\Rightarrow \lim_{t \to 0} \frac{1}{t} P_t(x,y) = \tilde{P}(x,y)\lambda(x) + \lim_{t \to 0} \frac{\mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x)}{t}$$ 

Sabendo que $\tilde{P}(x,y)\lambda(x) = Q(x,y)$ e demonstrando que o termo do segundo salto é desprezível na ordem de $t$, ou seja:

$$\lim_{t \to 0} \frac{1}{t} \mathbb{P}(\tilde{S}_2 \le t, X_t = y \mid X_0 = x) = 0$$

Temos, finalmente, que:

$$\lim_{t \to 0} \frac{1}{t} P_t(x,y) = Q(x,y), \text{para } x \neq y$$

---

### Demonstração Auxiliar: $\mathbb{P}(\tilde{S}_2 \le t \mid X_0 = x) = o(t)$

$$\mathbb{P}(\tilde{S}_2 \le t \mid X_0 = x) = \mathbb{P}\left(\frac{\mathcal{T_1}}{\lambda(\tilde{Z}_0)} + \frac{\mathcal{T_2}}{\lambda(\tilde{Z}_1)} \le t \;\middle|\; X_0 = x\right)$$

$$= \sum_{y \neq x} \mathbb{P}(\tilde{Z}_1 = y \mid \tilde{Z}_0 = x) \mathbb{P}\left(\frac{\mathcal{T_1}}{\lambda(x)} + \frac{\mathcal{T_2}}{\lambda(y)} \le t\right)$$

$$= \sum_{y \neq x} \tilde{P}(x,y) \int_{0}^{t} \lambda(x)e^{-\lambda(x)s} \mathbb{P}\left(\frac{\mathcal{T_2}}{\lambda(y)} \le t - s\right) ds$$

$$= \sum_{y \neq x} \tilde{P}(x,y) \int_{0}^{t} \lambda(x)e^{-\lambda(x)s} \left(1 - e^{-\lambda(y)(t - s)}\right) ds$$

$$= \sum_{y \neq x} \tilde{P}(x,y) \left[ \left(1 - e^{-\lambda(x)t}\right) - \lambda(x)e^{-\lambda(y)t} \int_{0}^{t} e^{-(\lambda(x) - \lambda(y))s} ds \right]$$

$$= \sum_{y \neq x} \tilde{P}(x,y) \Big[ (\lambda(x)t + o(t)) - (\lambda(x)t + o(t)) \Big]$$

$$= \sum_{y \neq x} \tilde{P}(x,y) \cdot o(t) = o(t)$$
