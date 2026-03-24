# Aula 6

**Data:** 20/03/2026

## 1. Revisão

$(X_t)_{t \ge 0}$ C.M. com matriz de transição $P$

$(X_t)_{t \ge 0}$ é <u>irredutível</u> se:
$\forall x, y \in \mathcal{X}, \exists t = t(x, y) \ge 0$ t.q.
$\mathbb{P}_x(X_t = y) = P^t(x, y) > 0$

Definimos,
$\mathcal{T}(x) = \{ t \ge 1 : P^t(x, x) > 0 \}$  
$\hookrightarrow$ conjunto de instantes de tempo em que a cadeia retorna ao ponto inicial $x$.

O <u>período</u> de $x$ é definido como $\text{mdc } \mathcal{T}(x)$

**Prop:** Todos os estados de uma C.M. irredutível têm o mesmo período.

**Prova.** Precisamos mostrar que $\text{mdc } \mathcal{T}(x) = \text{mdc } \mathcal{T}(y)$, $\forall x, y \in \mathcal{X}$.

Fixe $y$ e $x$ estados da cadeia e denote $d_y = \text{mdc } \mathcal{J}(y)$.

Vamos mostrar que $d_y$ divide todos os elementos de $\mathcal{T}(x)$, o que garante que $\text{mdc } \mathcal{T}(x) \ge d_y$.

Tome $t \in \mathcal{T}(x) \Rightarrow P^t(x, x) > 0$.

Pela <u>irredutibilidade</u> $\exists r, l \ge 0$ t.q. $P^r(x, y) > 0$ e $P^l(y, x) > 0$.

Logo, em $l + t + r$ passos a cadeia saindo de $y$ retorna a $y$ passando por $x$ com prob. positiva.

---

Logo, $t + l + r \in \mathcal{T}(y) \implies t + l + r = k_2 \cdot d_y$ para algum $k_2 \geq 1$ inteiro.  
Como $l + r \in \mathcal{T}(y) \implies l + r = k_1 \cdot d_y$, com $1 \leq k_1 \leq k_2$ inteiro.

Logo, $t = (k_2 - k_1) d_y \implies t$ é divisível por $d_y$  
$\implies d_y$ divide todos os elementos de $\mathcal{T}(x)$  
$\implies d_x = \text{MDC } \mathcal{T}(x) \geq d_y$

Usando que $l + r \in \mathcal{T}(x)$ e que $t + l + r \in \mathcal{T}(x)$ se $t \in \mathcal{T}(y)$, podemos concluir que:  
$d_y = \text{MDC } \mathcal{T}(y) \geq d_x$

---

## Observação:

Para mostrar que $l + r \in \mathcal{T}(y)$, precisamos mostrar que a probabilidade de transição em $l+r$ passos é estritamente positiva:

$$P^{l+r}(y,y) > 0$$

**Prova:**
Utilizando a propriedade de Chapman-Kolmogorov:

$$P^{l+r}(y,y) = P^{l}P^{r}(y,y) =\sum_{z \in \mathcal{X}} P^l(y,z) P^r(z,y) \geq P^l(y,x) P^r(x,y) > 0$$

Isso é verdade pois, se os estados se comunicam, existem caminhos com probabilidade positiva entre $y \to x$ (comprimento $l$) e $x \to y$ (comprimento $r$).

---

## 2. Equação de Chapman-Kolmogorov

De forma geral:

$$P^{t+s}(y,x) = \sum_{z \in \mathcal{X}} P^t(y,z) P^s(z,x)$$

$$\iff$$

$$\mathbb{P}_y(X_{t+s} = x) = \sum_{z \in \mathcal{X}} \mathbb{P}_y(X_t = z) \mathbb{P}(X_s = x)$$

> **Equação de Chapman-Kolmogorov**

---

Em C.M. **irredutível**, definimos o **período** da Cadeia como sendo o período comum a todos os estados.

A cadeia é **Aperiódica** se todos os estados têm período 1.

---
## 3. Distribuição Estacionária em Espaços Gerais ($\mathcal{X}$ Finito)

### Teorema:

$(X_t)_{t \geq 0}$ C.M. com matriz de transição $P$ e distribuição inicial $\nu$. Para cada $T > 1$, considere

$$Q_T = \frac{1}{T} (I + P + P^2 + \dots + P^{T-1}) = \frac{1}{T} \sum_{t=0}^{T-1} P^t$$

e

$$\nu_T = \nu \cdot Q_T$$

Então existe um vetor de probabilidade $\pi$ tal que:

$$\pi = \pi P \quad \text{e} \quad \boxed{\pi = \lim_{T \to \infty} \nu_T}$$

Se, além disso, $P$ é **irredutível**, então $\pi$ é **único** e $\pi(x) > 0$ para todo $x \in \mathcal{X}$.

## Interpretação Probabilística da Distribuição Estacionária

### Interpretação:

$$
\begin{aligned}
\pi(y) &= \lim_{T \to \infty} \nu_T(y) = \lim_{T \to \infty} \nu Q_T(y) \\
&= \lim_{T \to \infty} \sum_{x \in \mathcal{X}} \nu(x) Q_T(x,y) \\
&= \lim_{T \to \infty} \sum_{x \in \mathcal{X}} \nu(x) \frac{1}{T} \sum_{t=0}^{T-1} P^t(x,y) \\
&= \lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} \sum_{x \in X} \nu(x) P^t(x,y) \\
&= \lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} \nu P^t(y) \\
&= \lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} \mathbb{P}_{\nu}(X_t = y) \\
&= \lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} \mathbb{E}_{\nu} [ \mathbb{1}_{\{X_t = y\}} ] \\
&= \lim_{T \to \infty} \mathbb{E}_{\nu} \left[ \frac{1}{T} \sum_{t=0}^{T-1} \mathbb{1}_{\{X_t = y\}} \right]
\end{aligned}
$$

## 4. Estimadores e o Teorema Ergódico

### Denotando:

$$\hat{N}_{T-1}(y) = \sum_{t=0}^{T-1} \mathbb{1}_{\{X_t = y\}}$$
> Número de vezes que a cadeia visita o estado $y$

temos:

$$\pi(y) = \lim_{T \to \infty} \mathbb{E}_{\nu} \left[ \frac{\hat{N}_{T-1}(y)}{T} \right]$$

O estimador $\frac{\hat{N}_{T-1}(y)}{T}$ é **assintoticamente não-viesado** para $\pi(y)$.

---

### O Teorema Ergódico (a ser visto mais adiante)

$\frac{\hat{N}_{T-1}(y)}{T}$ é um **estimador consistente** para $\pi(y)$, se $P$ é **irredutível**.

> Com prob. 1 a convergência ocorre (ser consistente)

$$\mathbb{P}_{\nu} \left( \lim_{T \to \infty} \frac{\hat{N}_{T-1}(y)}{T} = \pi(y) \right) = 1$$

---

### Prova: O Limite da Média Ergódica é uma Distribuição Estacionária

**Afirmação:** $\pi = \lim_{T \to \infty} \nu_T$ é uma distribuição estacionária.

Prova:

Para ser uma distribuição estacionária, devemos mostrar que $\pi P = \pi$.

$$
\begin{aligned}
\pi P &= \left( \lim_{T \to \infty} \nu_T \right) P = \left( \lim_{T \to \infty} \nu Q_T \right) P \\
&= \lim_{T \to \infty} (\nu Q_T P) = \lim_{T \to \infty} \nu \left( \frac{1}{T} \sum_{t=0}^{T-1} P^t \right) P \\
&= \lim_{T \to \infty} \nu \left( \frac{1}{T} \sum_{t=1}^{T} P^t \right) \\
&= \lim_{T \to \infty} \nu \left( \frac{1}{T} \left( \sum_{t=0}^{T-1} P^t - IP^T \right) \right) \\
&= \lim_{T \to \infty} \nu \left( Q_T - \frac{1}{T} I + \frac{1}{T} P^T \right) \\
&= \pi - \lim_{T \to \infty} \frac{1}{T} \nu + \lim_{T \to \infty} \frac{1}{T} \nu P^T \\
&= \pi - 0 + 0 = \pi
\end{aligned}
$$

---

> **Justificativa do limite:** $\frac{\nu P^T(y)}{T} = \frac{\mathbb{P}_{\nu}(X_T = y)}{T} \leq \frac{1}{T}$.
> Como $\frac{1}{T} \to 0$ quando $T \to \infty$, o termo desaparece.