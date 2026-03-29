# Aula 9

**Data:** 27/03/2026

## Revisão
Seja $(X_t)_{t \ge 0}$ C.M. com período $d > 1$, matriz $P$ irredutível e distribuição estacionária $\pi$.

Sejam $\mathcal{X}_1, \dots, \mathcal{X}_d$ uma partição de $\mathcal{X}$ tais que:  

* $\mathbb{P}_x(X_1 \in \mathcal{X}_{r+1}) = 1, \forall x \in \mathcal{X}_r, 1 \le r \le d-1$
* $\mathbb{P}_x(X_1 \in \mathcal{X}_1) = 1, \forall x \in \mathcal{X}_d$

Então: $\pi(y) = \frac{\pi_r(y)}{d}, \quad \forall y \in \mathcal{X}_r$  
Onde $\pi_r$ é a única medida de probabilidade estacionária para a cadeia $(X_{td})_{t \ge 0}$ restrita a $\mathcal{X}_r$.

Para mostrar esse resultado, usamos o seguinte:

$$\lim_{t \to \infty} \frac{P^t(x, y) + P^{t+1}(x, y) + \dots + P^{t+d-1}(x, y)}{d} = \pi(y),\quad \forall x,y \in \mathcal{X}$$

Prova: Tome $y \in \mathcal{X}_r$ e escolha $x \in \mathcal{X}_1$. Note que:

$$\lim_{t \to \infty} \frac{P^t(x,y) + P^{t+1}(x,y) + \dots + P^{t+d-1}(x,y)}{d} = \lim_{t \to \infty} \frac{P^{md+(r-1)}(x,y)}{d}$$

Pela equação de Kolmogorov:

$$= \frac{1}{d} \lim_{m \to \infty} \sum_{z \in \mathcal{X}_r} P^{d+r-1}(x,z) P^{(m-1)d}(z,y)$$

$$= \frac{1}{d} \sum_{z \in \mathcal{X}_r} P^{d+r-1}(x,z) \lim_{m \to \infty} P^{(m-1)d}(z,y)$$

$$= \frac{1}{d} \sum_{z \in \mathcal{X}_r} P^{d+r-1}(x,z) \cdot \pi_r(y) = \frac{\pi_r(y)}{d}$$

> A cadeia $(X_{td})_{t \ge 0}$, restrita a $\mathcal{X}_r$, é irredutível e aperiódica. 
> Isso ocorre pois $\mathbb{P}_x(X_{d+r-1} \in \mathcal{X}_r) = 1$.[Verificar]

---

## Teorema de Convergência
Se $(X_t)_{t \ge 0}$ é uma C.M. irredutível, aperiódica, com matriz de transição $P$ e distribuição estacionária $\pi$.
Então

$$d(t) = \max_{x \in \mathcal{X}} \|P^t(x, \cdot) - \pi\|_{VT} \le C \cdot \alpha^t$$ 

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;para $C > 0$ e $\alpha \in (0, 1)$.

---

## Tempo de Mistura (Mixing Time)
Fixe $\varepsilon > 0$, definimos:

$$t_{mix}(\varepsilon) = \min\{t \ge 0 : d(t) \le \varepsilon\}$$

O tempo de mistura de referência é $t_{min}(\varepsilon)$ para $\varepsilon = 1/4$:

$$t_{min} := t_{mix}(1/4)$$

**Proposição:** $t_{mix}(\varepsilon) \le t_{mix} \lceil \log_2(\varepsilon^{-1}) \rceil$.

**Exemplo:** P.A.P.(Preguiçoso) no anel com $n$ vértices:

$$\frac{n^2}{32} \le t_{mix} \le n^2$$

---

## Acoplamento de Cadeias de Markov
Um acoplamento de cadeias de Markov com matriz $P$ é um processo $(X_t, Y_t)_{t \ge 0}$, com a propriedade que, ambos os processos $(X_t)_{t \ge 0}$ e $(Y_t)_{t \ge 0}$ são cadeias de Markov com matriz $P$.

Qualquer acoplamento pode ser modificado de forma que:

($\bigtriangleup$) $X_{t_*} = Y_{t_*} \implies X_t = Y_t, \quad \forall t \ge t_*$

>$\hookrightarrow$ uma vez que se encontram, permanecem juntos

### Teorema do Acoplamento
Dado um acoplamento $(X_t, Y_t)_{t \ge 0}$ satisfazendo ($\bigtriangleup$) para o qual $X_0 = x$ e $Y_0 = y$.
Seja $\mathcal{T}_c = \min\{t \ge 0 : X_t = Y_t\}$ o **tempo de coalescência**.

Então:

$$\|P^t(x, \cdot) - P^t(y, \cdot)\|_{VT} \le \mathbb{P}_{x,y}(\mathcal{T}_c > t)$$

onde $\mathbb{P}_{x,y}$ denota a **medida de probabilidade** sob a qual as cadeias $(X_t)_{t \ge 0}$ e $(Y_t)_{t \ge 0}$ estão definidas e $\mathbb{P}_{x,y}(X_0 = x) = 1 = \mathbb{P}_{x,y}(Y_0 = y)$

Logo,

$$d(t) \le \bar{d}(t) = \max_{x,y}\|P^t(x, \cdot) - P^t(y, \cdot)\|_{VT} \le \max_{x,y}\mathbb{P}_{x,y}(\mathcal{T}_c > t) \le \max_{x,y}\frac{\mathbb{E}_{x,y}[\mathcal{T}_c]}{t}$$ 

Aplicando a desigualdade de Markov para $t_* = 4 \max_{x,y} \mathbb{E}_{x,y}[\mathcal{T}_c]$:

$$\implies d(t_*) \le \frac{1}{4} \implies t_{mix} \le 4 \max_{x,y} \mathbb{E}_{x,y}[\mathcal{T}_c]$$