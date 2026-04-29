# LISTA 3

### Exercício 1
Considere uma Cadeia de Markov irredutível $(X_t)_{t \ge 0}$ e defina $\mathcal{T}_x^{+,k} = \min \{ t \ge \mathcal{T}_x^{+,k-1} + 1 : X_t = x \}$, $k \ge 1$, com $\mathcal{T}_x^{+,0} = 0$ e $x \in \mathcal{X}$. Mostre que os blocos $(X_{\mathcal{T}_x^{+,k-1}}, \dots, X_{\mathcal{T}_x^{+,k}-1})$, $k \ge 1$, são independentes e identicamente distribuídos.

---

### Exercício 2
Considere uma cadeia de Markov $(X_t)_{t \ge 0}$ com espaço de estados $\mathcal{X}$ e matriz de transição $P$. Para $L \ge 1$, defina $Y_t = (X_t, X_{t+1}, \dots, X_{t+L})$. O processo $(Y_t)_{t \ge 0}$ toma valores em $\mathcal{Y} = \{ (x_0, \dots, x_L) \in \mathcal{X}^{L+1} : P(x_0, x_{1}), \dots, P(x_{L-1}, x_{L}) > 0 \}$.

**a)** Prove que $(Y_t)_{t \ge 0}$ é uma cadeia de Markov e forneça a sua matriz de transição.

**b)** Mostre que se $(X_t)_{t \ge 0}$ é irredutível, então $(Y_t)_{t \ge 0}$ também é irredutível.

**c)** Mostre que se $(X_t)_{t \ge 0}$ tem uma distribuição estacionária, então $(Y_t)_{t \ge 0}$ também tem uma distribuição estacionária.

---

### Exercício 3
Seja $(X_t)_{t \ge 0}$ uma cadeia de Markov com matriz de transição $P$ e espaço de estados $\mathcal{X}$. Suponha que $P(X_0 = x) = \pi(x) > 0$ para todos os estados $x \in \mathcal{X}$, onde $\pi$ é uma distribuição estacionária. Defina a matriz $Q = (Q(x,y))_{x,y \in \mathcal{X}}$ como:

$$Q(x,y) = \frac{\pi(y)P(y,x)}{\pi(x)}$$

Construa o processo $(X_{-t})_{t \ge 1}$ por:

$$\mathbb{P}(X_{-t}=x_t, \dots, X_{-2}=x_2, X_{-1}=x_1 | X_0=x,X_1=y_1, \dots, X_s=y_s)$$

$$ = \mathbb{P}(X_{-t}=x_t, \dots, X_{-2}=x_2, X_{-1}=x_1 | X_0=x)$$

$$ = Q(x, x_1)Q(x_1, x_2)\dots Q(x_{t-1}, x_t), $$

$$\forall t \ge 1, s \ge 1, x,x_1,\dots,x_t,y_1,\dots,y_s \in \mathcal{X}$$

Mostre que $(X_t)_{t \in \mathbb{Z}}$ é uma Cadeia de Markov com matriz de transição $P$ e tal que $\mathbb{P}(X_t = x) = \pi(x)$ para todo $x \in \mathcal{X}$ e todo $t \in \mathbb{Z}$.

---

### Exercício 4
Seja $(X_t)_{t \ge 0}$ uma cadeia de Markov irredutível com espaço de estados finito e matriz de transição $P$. Denote $\pi$ a distribuição estacionária e considere $g: \mathcal{X}^{L+1} \to \mathbb{R}$. Usando o Teorema Ergódico e o Exercício 2, mostre que para qualquer distribuição inicial $\mu$:

$$\lim_{t \to \infty} \frac{1}{t+1} \sum_{s=0}^{t} g(X_t, \dots, X_{t+L}) = \sum_{(x_0, \dots, x_L) \in \mathcal{X}^{L+1}} g(x_0, \dots, x_L) \pi(x_0) \prod_{i=0}^{L-1} P(x_i, x_{i+1})$$

$\mathbb{P}_\mu$-quase certamente.