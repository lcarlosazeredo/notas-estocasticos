# Aula 36

 **Data:** 17/06/2026

### Teorema 1:

Seja $X$ uma C.M. **irredutível**. As seguintes afirmações são equivalentes:

1. Cada $x \in \mathcal{X}$ é **recorrente positivo**.
2. Algum estado $x \in \mathcal{X}$ é **recorrente positivo**.
3. $X$ não tem explosões e possui distribuição estacionária $\pi_X$.

Além disso,

$$\pi_X(x) = \frac{1}{\lambda_x \mathbb{E}_x[\mathcal{T}_{x,x}^+]}$$

Onde:

* $\mathcal{T}_{x,x}^+ = \inf\{t \ge \tilde{S}_1 : X_t = x\}$ 
* $\tilde{S}_1 = \inf\{t > 0 : X_t \neq X_0\}$

---

Se: $\tilde{\pi}_X(x) = \mathbb{E}_{x_0}\left[\int_0^{\mathcal{T}_{x,x_0}^+ \wedge J} \mathbb{1}_{\{X_t = x\}} dt\right]$

onde $J = \lim_{n \to \infty} \tilde{S}_n$ com $x_0 \in \mathcal{X}$ fixado, $\forall x \in \mathcal{X}$.

Então,

1. $\sum_{x \in \mathcal{X}} \tilde{\pi}_X(x) = \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^+ \wedge J]$
2. $\tilde{\pi}_X(x) = \frac{1}{\lambda_x} \tilde{\pi}_\tilde{Z}(x) \iff \tilde{\pi}_\tilde{Z} = \tilde{\pi}_X \Lambda$

Em particular,

$$\tilde{\pi}_X(x_0) = \frac{\tilde{\pi}_\tilde{Z}(x_0)}{\lambda_{x_0}} = \frac{1}{\lambda_{x_0}}$$

---

#### Prova:

**(1) $\implies$ (2)** $\checkmark$ 

**(2) $\implies$ (3)** Neste caso, temos que: 

$$\sum_{x \in \mathcal{X}} \tilde{\pi}_X(x) = \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^+] < \infty$$ 

Como: 

$$0 = \tilde{\pi}_\tilde{Z}(\tilde{P} - I) = \tilde{\pi}_X \Lambda (\tilde{P} - I) = \tilde{\pi}_X Q$$ 

Logo, $\pi_X(x) = \frac{\tilde{\pi}_X(x)}{\mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^+]}$ é uma medida de probabilidade.

E satisfaz: 

$$\pi_X(x_0) = \frac{\tilde{\pi}_X(x_0)}{\mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^+]} = \frac{1}{\lambda_{x_0} \mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^+]}$$ 

Para provar **(3) $\implies$ (1)**: 

Vamos usar o seguinte resultado sobre C.M. em tempo discreto.

#### Proposição 3

Seja $P$ irredutível. Se $\mu$ for uma medida estacionária tal que $\mu(x_0) = 1$, então $\mu(x) \ge \tilde{\pi}(x), \forall x \in \mathcal{X}$.


Seja $\pi_X$ distribuição estacionária de $X$. Então $\pi_X \Lambda$ é uma medida estacionária para $\tilde{P}$: 

$$0 = \pi_X Q = \pi_X \Lambda (\tilde{P} - I)$$

Aplicando a Proposição 3 com $\mu(x) = \frac{\pi_X \Lambda(x)}{\pi_X \Lambda(x_0)} = \frac{\pi_X(x)\lambda_x}{\pi_X(x_0)\lambda_{x_0}}$, temos $\mu(x) \ge \tilde{\pi}_\tilde{Z}(x), \forall x \in \mathcal{X}$.
Logo,

$$\mathbb{E}_{x_0}[\mathcal{T}_{x,x_0}^+] = \sum_{x \in \mathcal{X}} \tilde{\pi}_X(x) = \sum_{x \in \mathcal{X}} \frac{\tilde{\pi}_Z(x)}{\lambda_x}$$ 

$$\le \sum_{x \in \mathcal{X}} \frac{1}{\lambda_x} \frac{\pi_X(x)\lambda_x}{\pi_X(x_0)\lambda_{x_0}}$$ 

$$= \frac{1}{\pi_X(x_0)\lambda_{x_0}} \sum_{x \in \mathcal{X}} \pi_X(x)$$ 

$$= \frac{1}{\pi_X(x_0)\lambda_{x_0}} < \infty$$

---

### Proposição 4 

Seja $X$ uma C.M. **irredutível** e **recorrente** com cadeia imersa $\tilde{Z}$.

Se $X$ é **recorrente positiva** com dist. estacionária $\pi_X$, então $\tilde{Z}$ é **recorrente positiva** $\iff \sum_{x \in \mathcal{X}} \lambda_x \pi_X(x) = C < \infty$. 
E neste caso a sua dist. estacionária é:

$$\pi_\tilde{Z}(x) = \frac{\lambda_x \pi_X(x)}{C}$$

Reciprocamente, se $\tilde{Z}$ é **recorrente positiva** com dist. estacionária $\pi_\tilde{Z}$, então $X$ é **recorrente positiva** $\iff \sum_{x \in \mathcal{X}} \frac{\pi_\tilde{Z}(x)}{\lambda_x} = C < \infty$.
E neste caso a sua dist. estacionária é:

$$\pi_X(x) = \frac{\pi_\tilde{Z}(x)}{\lambda_x C}$$

---

### Proposição 5 

Sob as condições e notações da Proposição 3, se além disso a cadeia é **recorrente**, então $\mu = \tilde{\pi}$.

#### Prova da Proposição 4: 

Se $X$ é recorrente positiva com dist. estacionária $\pi_X$, então $\pi_X Q = 0$.

Defina:

$$\mu = \frac{\pi_X \Lambda}{\pi_X \Lambda(x_0)}$$

Logo, $\mu$ é medida estacionária para $\tilde{P}$. Como $\tilde{Z}$ é recorrente, a Proposição 5 nos diz que $\mu = \tilde{\pi}_\tilde{Z}$.
Logo,

$$\sum_{x \in \mathcal{X}} \tilde{\pi}_\tilde{Z}(x) = \sum_{x \in \mathcal{X}} \mu(x) = \sum_{x \in \mathcal{X}} \frac{\pi_X(x)\lambda_x}{\pi_X(x_0)\lambda_{x_0}} = \frac{C}{\pi_X(x_0)\lambda_{x_0}}$$

Portanto,

$$\pi_\tilde{Z} = \frac{\tilde{\pi}_\tilde{Z}}{C} \pi_X(x_0)\lambda_{x_0} = \mu \frac{\pi_X(x_0)\lambda_{x_0}}{C}$$

$$= \left(\frac{\pi_X \Lambda}{\pi_X(x_0)\lambda_{x_0}}\right) \frac{\pi_X(x_0)\lambda_{x_0}}{C} = \frac{\pi_X \Lambda}{C}$$

---

## Comportamento Assintótico e Reversibilidade

### Teorema 1 

Seja $X = (X_t)_{t \ge 0}$ uma C.M. **irredutível** com taxas de salto satisfazendo $\sup_{x \in \mathcal{X}} \lambda_x = \bar{\lambda} < \infty$. 
Então $\forall x, y \in \mathcal{X}$:

$$\lim_{t \to \infty} \mathbb{P}_x(X_t = y) = \frac{1}{\lambda_y \mathbb{E}_y[\mathcal{T}_{x,y}^+]}$$

Em particular, se a cadeia for **recorrente nula**, temos $\mathbb{E}_y[\mathcal{T}_{x,y}^+] = \infty$ e o limite acima vale $0$.

Se a cadeia for **recorrente positiva** com dist. estacionária $\pi$, então:

$$\lim_{t \to \infty} \mathbb{P}_x(X_t = y) = \pi(y), \quad \forall x, y \in \mathcal{X}$$

#### Prova: 

Fixe $\delta > 0$ e considere o processo $X_\delta = (X_{n\delta})_{n \ge 0}$.

Pode-se mostrar que $X_\delta$ é uma cadeia de Markov em tempo discreto, irredutível, e que se $X$ é recorrente positiva com dist. estacionária $\pi$, então $X_\delta$ é recorrente positiva com dist. estacionária $\pi$.

Logo, $\forall x, y \in \mathcal{X}$:

$$\lim_{n \to \infty} P_{n\delta}(x, y) = \lim_{n \to \infty} (P_\delta)^n(x, y) = \pi(y)$$

Assim, fixado $x, y \in \mathcal{X}$ e $\varepsilon > 0$, $\exists n_0 = n_0(x,y,\varepsilon) > 0$ tal que:

$$\forall n \ge n_0 \quad |P_{n\delta}(x, y) - \pi(y)| < \varepsilon \quad (\star)$$

Por outro lado, dado $t > 0$, defina $n_t = \lfloor \frac{t}{\delta} \rfloor$ e note que $n_t \delta \le t < (n_t + 1)\delta$.
Pelo Teorema do Valor Médio:

$$|P_t(x, y) - P_{n_t\delta}(x, y)| = |P'_{\xi_t}(x, y)| |t - \delta n_t|$$ 

$$\le \delta |Q P_{\xi_t}(x, y)|$$

$$\le \delta \left( \max_{n_t \delta < \xi_t} |Q P_{\xi_t}(x,y)| \right) \le 2 \bar{\lambda} \delta$$

Pois:

$$|Q P_{\xi_t}(x, y)| = \left|\sum_z Q(x, z) P_{\xi_t}(z, y)\right|$$ 

$$= \left|\sum_{z \neq x} Q(x, z) P_{\xi_t}(z, y) + Q(x, x) P_{\xi_t}(x, y)\right|$$

$$\le \sum_{z \neq x} Q(x, z) P_{\xi_t}(z, y) + |Q(x, x)| P_{\xi_t}(x, y)$$ 

$$= 2\lambda_x \le 2\bar{\lambda}$$

Para concluir, dado $\varepsilon > 0$, escolha $\delta < \frac{\varepsilon}{\bar{\lambda}}$ e depois escolha $n_0$ tal que $(\star)$ valha, de modo que para $n_t \ge n_0$:

$$|P_t(x, y) - \pi(y)| \le |P_t(x, y) - P_{n_t\delta}(x, y)| + |P_{n_t\delta}(x, y) - \pi(y)|$$ 

$$\le 2\varepsilon + \varepsilon = 3\varepsilon$$

Como $\varepsilon > 0$ é arbitrário:

$$\lim_{t \to \infty} P_t(x, y) = \pi(y)$$