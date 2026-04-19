# Aula 15

**Data:** 13/04/2026

## Revisão
* $N(x) = \sum_{t=0}^{\infty} \mathbb{1}_{\{X_t = x\}}$, para $x \in \mathcal{X}$.
* **Definição:** Um estado $x$ é **recorrente** se $\mathbb{P}_x(N(x) = \infty) = 1$.
* **Recorrência:** $\mathbb{P}_x(N(x) = \infty) = 1 \iff \mathbb{P}_x(\mathcal{T}_x^+ < \infty) = 1$, onde:

    $$\mathcal{T}_x^+ = \min\{t \ge 1 : X_t = x\} $$

### Proposição
$Prop.:$ Em uma Cadeia de Markov **irredutível**, temos que $\mathbb{E}_y[\mathcal{T}_y^+] < \infty$, $\forall x, y \in \mathcal{X}$.

* Em particular, tomando $y=x$: $\mathbb{E}_x[\mathcal{T}_x^+] < \infty \Rightarrow \mathbb{P}_x(\mathcal{T}_x^+ < \infty) = 1$.
* $\implies$ todos os estados são **recorrentes**.

---

### Afirmação 1 (AF1)
Existem $r \ge 1$ e $\varepsilon > 0$ tais que:

$$\mathbb{P}_x\left(\bigcup_{s=1}^{r} \{X_{t+s} = y\} \mid X_t = z\right) > \varepsilon $$

Para todo $t \ge 0$ e $x, y, z \in \mathcal{X}$.

**Note que:** 

$\mathbb{E}_y[\mathcal{T}_y^+] = \sum_{t=0}^{\infty} \mathbb{P}_x(\mathcal{T}_y^+ > t) = \sum_{k=0}^{\infty} \sum_{t=kr}^{(k+1)r-1} \mathbb{P}_x(\mathcal{T}_y^+ > t) \le r \sum_{k=0}^{\infty} \mathbb{P}_x(\mathcal{T}_y^+ > kr)$

### Afirmação 2 (AF2)
$$\mathbb{P}_x(\mathcal{T}_y^+ > kr) \le (1 - \varepsilon)^k$$

Pela AF2, temos que:

$$\mathbb{E}_x[\mathcal{T}_y^+] \le r \sum_{k=0}^{\infty} (1 - \varepsilon)^k = \frac{r}{1 - (1 - \varepsilon)} = \frac{r}{\varepsilon}$$

---

### Prova da AF2
$$\mathbb{P}_x(\mathcal{T}_y^+ > kr) = \mathbb{P}_x\left(\mathcal{T}_y^+ > (k-1)r, \bigcap_{s=1}^{kr} \{X_{(k-1)r+s} \neq y\}\right)$$

$$= \mathbb{P}_x(\mathcal{T}_y^+ > (k-1)r, A_{(k-1)r+1}^c)$$

$$= \sum_{z \in \mathcal{X}, z \neq y} \mathbb{P}_x(\mathcal{T}_y^+ > (k-1)r, X_{(k-1)r} = z, A_{(k-1)r+1}^c)$$

Usando a propriedade de Markov e a AF1 com $t = (k-1)r$

$$\mathbb{P}_x(\mathcal{T}_y^+ > kr) \le \sum_{z \in \mathcal{X}, z \neq y} \mathbb{P}_x(\mathcal{T}_y^+ > (k-1)r, X_{(k-1)r} = z) \cdot (1 - \varepsilon)$$

$$= (1 - \varepsilon) \cdot \mathbb{P}_x(\mathcal{T}_y^+ > (k-1)r)$$

$Def.: x$ é **transiente** se $\mathbb{P}_x(N(x) < \infty) > 0$.

---

## Teorema Ergódico
* $\mathcal{X}$ Finito.
* $\mu = (\mu(x))_{x \in \mathcal{X}}$ vetor de probabilidade em $\mathcal{X}$.
* $f: \mathcal{X} \to \mathbb{R}$, onde $E_\mu[f] = \sum_{x \in \mathcal{X}} \mu(x)f(x)$.

### Enunciado
Fixa $f: \mathcal{X} \to \mathbb{R}$ qualquer. Se $(X_t)_{t \ge 0}$ é uma C.M. irredutível com distribuição estacionária $\pi$, então para qualquer distribuição inicial $\mu$:

$$\mathbb{P}_\mu \left( \lim_{t \to \infty} \frac{1}{t} \sum_{s=0}^{t-1} f(X_s) = \mathbb{E}_\pi[f] \right) = 1$$

---

**Caso particular:**
Se $f_x(y) = \begin{cases} 1, & y = x \\ 0, & c.c. \end{cases}$

Nesse caso,

&emsp;&emsp;$E_\pi[f_x] = \sum_{y} \pi(y) f_x(y) = \pi(x) f_x(x) = \pi(x)$

&emsp;e

&emsp;&emsp;$\frac{1}{t} \sum_{s=0}^{t-1} f_x(X_s) = \frac{1}{t} \sum_{s=0}^{t-1} \mathbb{1}_{\{X_s = x\}}$

---
### Esboço da Prova

Suponha que $\mu = \delta_x$ 

Defina, $\mathcal{T}_x^{+,0} = 0$ 
e 
$\mathcal{T}_x^{+,k} = \min \{t \ge \mathcal{T}_x^{+,k-1} + 1 : X_t = x\}$ 

---

Pela Prop. Forte de Markov, os blocos 

$$(X_{\mathcal{T}_x^{+,0}}, \dots, X_{\mathcal{T}_x^{+,1}-1}), (X_{\mathcal{T}_x^{+,1}}, \dots, X_{\mathcal{T}_x^{+,2}-1}), \dots, (X_{\mathcal{T}_x^{+,k}}, \dots, X_{\mathcal{T}_x^{+,k+1}-1}), \dots$$

são **i.i.d.**

---
Defina, $Y_k = \sum_{s=\mathcal{T}_x^{+,k-1}}^{\mathcal{T}_x^{+,k}-1} f(X_s)$ 

Logo, $(Y_k)_{k \ge 1}$ é seq. **i.i.d.**

