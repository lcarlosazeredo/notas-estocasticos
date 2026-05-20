# Aula 23

**Data:** 13/05/2026

### Resumo: Critério para recorrência

$x \in \mathcal{X}$ é **recorrente** $\iff S(x) = \displaystyle\sum_{t=0}^{\infty} P^t(x,x) = \infty$

---

### Teorema:
Se os estados $x$ e $y$ se comunicam, então ou $x$ e $y$ são **recorrentes**, ou $x$ e $y$ são **transientes**.

### Corolário:
Em uma cadeia irredutível, todos os estados são **recorrentes**, ou todos os estados são **transientes**.

**Prova:**
Existem $t_1 = t_1(x,y)$ e $t_2 = t_2(x,y)$ tais que $P^{t_1}(x,y) > 0$ e $P^{t_2}(y,x) > 0$. Note que, para todo $t \ge 0$:

$$P^{t_1 + t + t_2}(x,x) \ge P^{t_1}(x,y) P^t(y,y) P^{t_2}(y,x)$$

Denotando $\alpha = P^{t_1}(x,y) P^{t_2}(y,x) > 0$, temos:

$$P^{t_1 + t + t_2}(x,x) \ge \alpha P^t(y,y)$$

Logo,

$$S(x) \ge \sum_{t=0}^{\infty} P^{t_1 + t + t_2}(x,x) \ge \sum_{t=0}^{\infty} \alpha P^t(y,y) = \alpha S(y)$$

E, de modo similar, trocando os papéis de $x$ e $y$:

$$S(y) \ge \alpha S(x)$$

Assim,

$$\frac{1}{\alpha} S(x) \ge S(y) \ge \alpha S(x)$$

Isso implica que ambas as séries $\sum_{t=0}^{\infty} P^t(x,x)$ e $\sum_{t=0}^{\infty} P^t(y,y)$ convergem ou divergem simultaneamente.

---

### Medida Estacionária e Recorrência

Na prova do Teorema Ergodico no caso de $\mathcal{X}$ finito e a cadeia irredutível, vimos que a única distribuição de probabilidade estacionária $\pi$ pode ser escrita como:

$$\pi(y) = \frac{\mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right]}{\mathbb{E}_x[\mathcal{T}_x^+]}, \quad \forall y \in \mathcal{X}$$

onde $x \in \mathcal{X}$ é um estado arbitrário e $\mathcal{T}_x^+ = \min\{t \ge 1 : X_t = x\}$.

O lado direito define uma medida de probabilidade pois:

1. $\mathbb{E}_x[\mathcal{T}_x^+] < \infty$
2. $\displaystyle\sum_{y \in \mathcal{X}} \mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right] = \mathbb{E}_x[\mathcal{T}_x^+]$

Além disso, para provar tal representação $\pi$, definimos o vetor $\tilde{\pi}(y) = \mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^+ - 1} \mathbb{1}_{\{X_t = y\}} \right]$,$ y \in \mathcal{X}$, e provamos que:

$$\tilde{\pi} P(y) = \tilde{\pi}(y), \forall y \in \mathcal{X}$$

---

O item 1 não é em geral verdade se o espaço de estados for infinito. Entretanto, o vetor $\tilde{\pi}$ definido acima continua bem definido e satisfaz a identidade $\tilde{\pi} P = \tilde{\pi}$ mesmo no caso de $\mathcal{X}$ enumerável e infinito, com:

$$\sum_{y \in \mathcal{X}} \tilde{\pi}(y) = \mathbb{E}_x[\mathcal{T}_x^+]$$

Quando $\mathbb{E}_x[\mathcal{T}_x^+] = +\infty$, o vetor $\tilde{\pi}$ define o que chamamos de **medida invariante** para a Cadeia.

#### Exemplo: P.A. em $\mathbb{Z}$
Considere o passeio aleatório em $\mathcal{X} = \mathbb{Z}$:

$$\tilde{\pi}(y) = 1, \quad \forall y \in \mathbb{Z} \quad \text{é medida invariante}$$

$$\tilde{\pi} P(y) = \sum_{x \in \mathbb{Z}} \tilde{\pi}(x) P(x,y) = \tilde{\pi}(y-1) P(y-1,y) + \tilde{\pi}(y+1) P(y+1,y)$$

$$= 1 \cdot p + 1 \cdot (1-p) = 1 = \tilde{\pi}(y)$$

---

### Teorema:
Uma cadeia irredutível e recorrente é **recorrente positiva** se, e somente se, a medida invariante $\tilde{\pi}$ satisfaz:

$$\sum_{y \in \mathcal{X}} \tilde{\pi}(y) < \infty$$

### Teorema:
Uma cadeia irredutível é **recorrente positiva** $\iff$ Existe uma medida de probabilidade estacionária $\pi$.

Além disso, quando existe, para todo $x \in \mathcal{X}$, $\pi$ é única e:

$$\pi(x) = \frac{1}{\mathbb{E}_x[\mathcal{T}_x^+]} > 0$$

*(Prova omitida)*

---

#### Exemplo: (P.A. com barreira refletora na origem)

$$P(0,y) = \begin{cases} 1 & \text{se } y = 1 \\ 0 & \text{c.c.} \end{cases}$$

$$P(x,y) = \begin{cases} p_x & \text{se } y = x + 1 \\ q_x & \text{se } y = x - 1 \\ 0 & \text{c.c.} \end{cases} \quad \text{para } x \ge 1, \text{ com } p_x + q_x = 1 \text{ e } p_x \in (0,1)$$

Neste exemplo, $\tilde{\pi}$ é uma medida estacionária se:

$$\tilde{\pi}(0) = \tilde{\pi}(1) q_1$$

$$\tilde{\pi}(x) = \tilde{\pi}(x-1) p_{x-1} + \tilde{\pi}(x+1) q_{x+1}, \quad x \ge 1$$

**Afirmação:** 

$$\tilde{\pi}(x) = \tilde{\pi}(0) \frac{p_0 p_1 \cdots p_{x-1}}{q_0 q_1 \cdots q_x}$$

A cadeia é **recorrente positiva**:

$$\sum_{x=0}^{\infty} \tilde{\pi}(x) < \infty \iff \tilde{\pi}(0) \left( 1 + \sum_{x=1}^{\infty} \frac{p_0 \cdots p_{x-1}}{q_0 \cdots q_x} \right) < \infty \iff 1 + \sum_{x=1}^{\infty} \frac{p_0 \cdots p_{x-1}}{q_0 \cdots q_x} < \infty$$

Neste caso, podemos definir uma distribuição de probabilidade estacionária $\pi$ normalizando a medida por:

$$\pi(0) = \frac{1}{1 + \displaystyle\sum_{x=1}^{\infty} \frac{p_0 \cdots p_{x-1}}{q_0 \cdots q_x}}$$

$$\pi(x) = \pi(0) \frac{p_0 \cdots p_{x-1}}{q_0 \cdots q_x}, \text{que é estacionária}$$