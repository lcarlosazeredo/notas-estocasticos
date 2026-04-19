# Aula 16

**Data:** 15/04/2026

## Revisão
* C.M. **irredutível**
* dist. estacionária **$\pi$**, única
* matriz de transição $P$

### Teorema Ergódico
Para qualquer função $f: \mathcal{X} \rightarrow \mathbb{R}$:

$$\mathbb{P}_{\mu} \left( \lim_{t \to \infty} \frac{1}{t+1} \sum_{s=0}^{t} f(X_s) = \mathbb{E}_{\pi}[f] \right) = 1$$

Para toda distribuição inicial $\mu$.

Onde $\mathbb{E}_{\pi}[f] = \sum_{x \in \mathcal{X}} f(x)\pi(x) = \mathbb{E}[f(X)], X \sim \pi$.

---

## Prova (Assumindo $\mu = \delta_x$ para $x$ arbitrário)


Usando a **Propriedade Forte**, podemos mostrar que os blocos:

$$(X_{\mathcal{T}_x^{+,0}}, \dots, X_{\mathcal{T}_x^{+,1}-1}), (X_{\mathcal{T}_x^{+,1}}, \dots, X_{\mathcal{T}_x^{+,2}-1}), \dots, (X_{\mathcal{T}_x^{+,k}}, \dots, X_{\mathcal{T}_x^{+,k+1}-1}), \dots$$

são **i.i.d.**.

Logo, definindo:

$$Y_k = \sum_{t=\mathcal{T}_x^{+,k-1}}^{\mathcal{T}_x^{+,k}-1} f(X_t), k \ge 1$$

temos que $(Y_k)_{k \ge 1}$ são **i.i.d.**.

### AF. 1: $\mathbb{E}_x[|Y_1|] < \infty$
### Prova da AF. 1

$$|Y_1| = \left| \sum_{t=\mathcal{T}_x^{+,0}}^{\mathcal{T}_x^{+,1}-1} f(X_t) \right| \le \sum_{t=\mathcal{T}_x^{+,0}}^{\mathcal{T}_x^{+,1}-1} |f(X_t)| \le \|f\|_{\infty} \mathcal{T}_x^{+,1}$$

Onde $\|f\|_{\infty} = \max_{x \in \mathcal{X}} |f(x)|$.

Implica que:

$$\mathbb{E}_x[|Y_1|] \le \mathbb{E}_x[\|f\|_{\infty} \mathcal{T}_x^{+,1}] = \|f\|_{\infty} \mathbb{E}_x[\mathcal{T}_x^{+,1}] < \infty$$

Pela **LGN**, sabemos que:

$$\mathbb{P}_x \left( \lim_{n \to \infty} \frac{1}{n} \sum_{k=1}^{n} Y_k = \mathbb{E}_x[Y_1] \right) = 1$$

Denote $S_t = \sum_{s=0}^{t-1} f(X_s)$. Com essa notação:

$$\mathbb{P}_x \left( \lim_{n \to \infty} \frac{1}{n} S_{\mathcal{T}_x^{+,n}} = \mathbb{E}_x[Y_1] \right) = 1$$

---

Por outro lado, lembre que a sequência $(\mathcal{T}_x^{+,k} - \mathcal{T}_x^{+,k-1})_{k \ge 1}$ é i.i.d. com média $\mathbb{E}_x[\mathcal{T}_x^{+,1}]$.
Logo, pela LGN:

$$\lim_{n \to \infty} \frac{\mathcal{T}_x^{+,n}}{n} = \lim_{n \to \infty} \frac{1}{n} \sum_{k=1}^{n} (\mathcal{T}_x^{+,k} - \mathcal{T}_x^{+,k-1}) = \mathbb{E}_x[\mathcal{T}_x^{+,1}]$$

Com prob. 1.



Como consequência:

$$\frac{S_{\mathcal{T}_x^{+,n}}}{\mathcal{T}_x^{+,n}} = \frac{(\frac{S_{\mathcal{T}_x^{+,n}}}{n})}{(\frac{\mathcal{T}_x^{+,n}}{n})} \xrightarrow{n \to \infty} \frac{\mathbb{E}_x[Y_1]}{\mathbb{E}_x[\mathcal{T}_x^{+,1}]}$$

Com prob. 1.

---

### AF. 2: $\mathbb{E}_x[Y_1] = \mathbb{E}_x \left[ \sum_{t=0}^{\mathcal{T}_x^{+,1}-1} f(X_t) \right] = \mathbb{E}_{\pi}[f] \mathbb{E}_x[\mathcal{T}_x^{+,1}]$

Supondo AF. 2 verdadeira, temos:

$$\mathbb{P}_x \left( \lim_{n \to \infty} \frac{S_{\mathcal{T}_x^{+,n}}}{\mathcal{T}_x^{+,n}} = \mathbb{E}_{\pi}[f] \right) = 1 \quad (\bigtriangleup)$$

Sabendo de $(\bigtriangleup)$, vamos concluir o resultado:

$$\left| \frac{S_{\mathcal{T}_x^{+,n}}}{\mathcal{T}_x^{+,n}} - \frac{S_t}{t} \right| = \left| \frac{1}{\mathcal{T}_x^{+,n}} \sum_{s=0}^{\mathcal{T}_x^{+,n}-1} f(X_s) - \frac{1}{t} \sum_{s=0}^{t-1} f(X_s) \right|$$

$$\le \left| \left( \frac{1}{\mathcal{T}_x^{+,n}} - \frac{1}{t} \right) \sum_{s=0}^{\mathcal{T}_x^{+,n}-1} f(X_s) \right| + \left| \frac{1}{t} \left( \sum_{s=0}^{\mathcal{T}_x^{+,n}-1} f(X_s) - \sum_{s=0}^{t-1} f(X_s) \right) \right|$$

$$\le \frac{|t - \mathcal{T}_x^{+,n}| \cdot \|f\|_{\infty}}{\mathcal{T}_x^{+,n}} + \frac{1}{t} \left| \sum_{s=t}^{\mathcal{T}_x^{+,n}-1} f(X_s) \right|$$

$$\le \|f\|_{\infty} \frac{(\mathcal{T}_x^{+,n} - \mathcal{T}_x^{+,n-1})}{\mathcal{T}_x^{+,n-1}} + \frac{1}{t} \|f\|_{\infty} (\mathcal{T}_x^{+,n} - t)$$

$$\le 2 \|f\|_{\infty} \frac{(\mathcal{T}_x^{+,n} - \mathcal{T}_x^{+,n-1})}{\mathcal{T}_x^{+,n-1}} = 2 \|f\|_{\infty} \frac{(\mathcal{T}_x^{+,n} - \mathcal{T}_x^{+,n-1})/n}{\mathcal{T}_x^{+,n-1}/n}$$

Finalmente, como com prob.1

$$\lim_{n \to \infty} \frac{\mathcal{T}_x^{+,n}}{n} = \mathbb{E}_x[\mathcal{T}_x^{+,1}]$$

$$\lim_{n \to \infty} \frac{\mathcal{T}_x^{+,n-1}}{n} = \lim_{n \to \infty} \frac{n-1}{n} \frac{\mathcal{T}_x^{+,n-1}}{n-1} = \mathbb{E}_x[\mathcal{T}_x^{+,1}]$$

Temos:

$$\left| \frac{S_t}{t} - \mathbb{E}_{\pi}[f] \right| \le \left| \frac{S_t}{t} - \frac{S_{\mathcal{T}_x^{+,n}}}{\mathcal{T}_x^{+,n}} \right| + \left| \frac{S_{\mathcal{T}_x^{+,n}}}{\mathcal{T}_x^{+,n}} - \mathbb{E}_{\pi}[f] \right| \xrightarrow{n \to \infty} 0$$

---

### Prova da AF. 2
$$\mathbb{E}_x \left[ \sum_{s=0}^{\mathcal{T}_x^{+,1}-1} f(X_s) \right] = \mathbb{E}_x \left[ \sum_{s=0}^{\mathcal{T}_x^{+,1}-1} \sum_{y \in \mathcal{X}} \mathbb{1}_{\{X_s = y\}} f(y) \right]$$

$$= \sum_{y \in \mathcal{X}} f(y) \cdot \mathbb{E}_x \left[ \sum_{s=0}^{\mathcal{T}_x^{+,1}-1} \mathbb{1}_{\{X_s = y\}} \right]$$

Para mostrar a AF. 2, basta provar que:

$$\pi(y) = \frac{\mathbb{E}_x \left[ \sum_{s=0}^{\mathcal{T}_x^{+,1}-1} \mathbb{1}_{\{X_s = y\}} \right]}{\mathbb{E}_x[\mathcal{T}_x^{+,1}]}, \quad \forall y \in \mathcal{X}$$

Em particular:

$$\pi(x) = \frac{1}{\mathbb{E}_x[\mathcal{T}_x^{+,1}]}$$