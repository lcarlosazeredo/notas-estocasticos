# Aula 22

**Data:** 11/05/2026

Denote $N_x^+ = \displaystyle\sum_{t=1}^{\infty} \mathbb{1}_{\{X_t = x\}}, \quad x \in \mathcal{X}$

> $\hookrightarrow$ o número de visitas após o tempo 0.

---

### Teorema 1:

$\forall x, y \in \mathcal{X}$,

$$\mathbb{P}_y(N_x^+ = n) = \begin{cases} 
\rho_{yx} \rho_{xx}^{n-1}(1 - \rho_{xx}) & \text{se } n \ge 1 \\ \\
1 - \rho_{yx} & \text{se } n = 0 
\end{cases}$$

onde $\rho_{yx} = \mathbb{P}_y(\mathcal{T}_x^+ < \infty)$

---

Assumindo o teorema,

$$\begin{aligned}
\mathbb{P}_y(N_x^+ \ge n + 1) &= \sum_{m=n+1}^{\infty} \mathbb{P}_y(N_x^+ = m) = \sum_{m=n+1}^{\infty} \rho_{yx} \rho_{xx}^{n-1}(1 - \rho_{xx}) \\ \\
&= \rho_{yx}(1 - \rho_{xx})\rho_{xx}^n \sum_{k=0}^{\infty} \rho_{xx}^k \\ \\
&= \rho_{yx}(1 - \rho_{xx})\rho_{xx}^n \frac{1}{(1 - \rho_{xx})} = \rho_{yx}\rho_{xx}^n
\end{aligned}$$

---

Logo, para $y = x$

$$\begin{aligned}
\mathbb{P}_x(N_x^+ = \infty) &= \lim_{n \to \infty} \mathbb{P}_x(N_x^+ > n) = \lim_{n \to \infty} \rho_{xx}\rho_{xx}^n \\ \\
&= \lim_{n \to \infty} \rho_{xx}^{n+1} = \begin{cases} 
1 & \text{se } \rho_{xx} = 1 \\ 
0 & \text{se } \rho_{xx} < 1 
\end{cases}
\end{aligned}$$

Além disso, $\mathbb{E}_x[N_x^+] = \displaystyle\sum_{n=0}^{\infty} n \mathbb{P}_x(N_x^+ = n)$

$$\begin{aligned}
&= \sum_{n=1}^{\infty} n \rho_{xx}^n(1 - \rho_{xx}) \\ \\
&= \rho_{xx} \underbrace{\sum_{n=1}^{\infty} n \rho_{xx}^{n-1}(1 - \rho_{xx})}_{\text{Média Geom}(1 - \rho_{xx})} \\ \\
&= \frac{\rho_{xx}}{1 - \rho_{xx}}
\end{aligned}$$

$$\Rightarrow \mathbb{E}_x[N_x^+] = \infty \iff \rho_{xx} = 1. \quad \text{Em particular,}$$

$$\mathbb{P}_x(N_x^+ = \infty) > 0 \Rightarrow \rho_{xx} = 1$$

$$\Rightarrow \mathbb{P}_x(N_x^+ = \infty) = 1$$

$$\rho_{xx} = \mathbb{P}_x(\mathcal{T}_x^+ < \infty) < 1 \iff \mathbb{E}_x[N_x^+] < \infty$$

---

Relembre que $x \in \mathcal{X}$ é **recorrente** se $\mathbb{P}_x(N_x^+ = \infty) = 1$.

Caso contrário, $x$ é **transiente**. Observando que se

$$\mathbb{P}_x(N_x^+ = \infty) < 1 \Rightarrow \rho_{xx} < 1 \Rightarrow \mathbb{P}_x(N_x^+ = \infty) = 0$$

---

### Teorema 2:

$x$ é **recorrente** $\iff \displaystyle\sum_{t=0}^{\infty} P^t(x,x) = \infty$

**Prova:**

$$\begin{aligned}
\mathbb{E}_x[N_x] &= \mathbb{E}_x\left[ \sum_{t=0}^{\infty} \mathbb{1}_{\{X_t = x\}} \right] = \sum_{t=0}^{\infty} \mathbb{E}_x[\mathbb{1}_{\{X_t = x\}}] \\ \\
&= \sum_{t=1}^{\infty} \mathbb{P}_x(X_t = x) = \sum_{t=1}^{\infty} P^t(x,x)
\end{aligned}$$

Se $x$ é **recorrente**, então $\mathbb{E}_x[N_x^+] = \infty$

$$\Rightarrow \sum_{t=1}^{\infty} P^t(x,x) = \infty \Rightarrow \sum_{t=0}^{\infty} P^t(x,x) = \infty$$

Como $P^0(x,x) = I(x,x) = 1$, então

$$\begin{aligned}
\sum_{t=0}^{\infty} P^t(x,x) = \infty &\Rightarrow \sum_{t=1}^{\infty} P^t(x,x) = \infty \\ \\
&\Rightarrow \mathbb{E}_x[N_x^+] = \infty \\ \\
&\Rightarrow \mathbb{P}_x(\mathcal{T}_x^+ < \infty) = \rho_{xx} = 1 \\ \\
&\Rightarrow \mathbb{P}_x(N_x^+ = \infty) = 1 \Rightarrow x \text{ é recorrente}
\end{aligned}$$

---

### Exemplo (P.A em $\mathbb{Z}$)

$$P(x,y) = \begin{cases} 
p & \text{se } y = x+1 \\ 
1-p & \text{se } y = x-1 \\ 
0 & \text{c.c.} 
\end{cases}$$

Para todo $t$ ímpar: $P^{2t+1}(0,0) = 0$

Para $t$ par:

$$\begin{aligned}
P^{2t}(0,0) &= \binom{2t}{t} p^t (1-p)^{2t-t} \\ \\
&= \frac{(2t)!}{t! \, t!} \big(p(1-p)\big)^t
\end{aligned}$$

---

**Fórmula de Stirling:**

$$t! \sim \left(\frac{t}{e}\right)^t \sqrt{2\pi t}$$

> $$\left(\text{i.e., } \lim_{t \to \infty} \frac{t!}{\left(\frac{t}{e}\right)^t \sqrt{2\pi t}} = 1\right)$$

Usando Stirling:

$$\frac{(2t)!}{(t!)^2} \sim \frac{\left(\frac{2t}{e}\right)^{2t} \sqrt{2\pi(2t)}}{\left[ \left(\frac{t}{e}\right)^t \sqrt{2\pi t} \right]^2} = \frac{2^{2t}\left(\frac{t}{e}\right)^{2t} \sqrt{4\pi t}}{\left(\frac{t}{e}\right)^{2t} 2\pi t} = \frac{4^t}{\sqrt{\pi t}}$$

Logo,

$$P^{2t}(0,0) \sim \frac{\big(4p(1-p)\big)^t}{\sqrt{\pi t}}$$

Se $4p(1-p) < 1$ $\big(\text{i.e., } p \neq \frac{1}{2}\big)$, então

$$\sum_{t=1}^{\infty} \frac{\big(4p(1-p)\big)^t}{\sqrt{\pi t}} < \infty \quad \text{e pelo Teorema 2}$$

$0$ é transiente

---

Agora, para $p = \frac{1}{2}$:

temos que $P^{2t}(0,0) \sim \frac{1}{\sqrt{\pi t}}$

$$\Rightarrow \sum_{t=0}^{\infty} P^t(0,0) = \sum_{t=0}^{\infty} P^{2t}(0,0) \sim \sum_{t=0}^{\infty} \frac{1}{\sqrt{\pi t}} = \infty$$

$$\Rightarrow 0 \text{ é recorrente}$$

$$\hookrightarrow \text{Teorema 2}$$

---

### Prova do Teorema 1:

Para $n = 0$:

$$\mathbb{P}_y(N_x^+ = 0) = \mathbb{P}_y(\mathcal{T}_x^+ = \infty) = 1 - \mathbb{P}_y(\mathcal{T}_x^+ < \infty) = 1 - \rho_{yx}$$

Suponha o resultado válido para todo $0 \le m \le n$. Em particular,

$$\begin{aligned}
\mathbb{P}_y(N_x^+ > n) &= 1 - \mathbb{P}_y(N_x^+ \le n) = 1 - \sum_{m=0}^{n} \mathbb{P}_y(N_x^+ = m) \\ \\
&= 1 - \left( (1 - \rho_{yx}) + \sum_{m=1}^{n} \rho_{yx} \rho_{xx}^{m-1} (1 - \rho_{xx}) \right) \\ \\
&= \rho_{yx} - \rho_{yx}(1 - \rho_{xx})\sum_{m=1}^{n} \rho_{xx}^{m-1} \\ \\
&= \rho_{yx} - \rho_{yx}(1 - \rho_{xx})\sum_{m=0}^{n-1} \rho_{xx}^m \\ \\
&= \rho_{yx} - \rho_{yx}(1 - \rho_{xx}) \frac{(1 - \rho_{xx}^n)}{1 - \rho_{xx}} \\ \\
&= \rho_{yx}\big(1 - (1 - \rho_{xx}^n)\big) \\ \\
&= \rho_{yx}\rho_{xx}^n
\end{aligned}$$

---

Denotando $\mathcal{T}_x^{+,n}$ o $n$-ésimo tempo de retorno ao estado $x$, temos que

$$\begin{aligned}
\mathbb{P}_y(N_x^+ = n+1) &= \mathbb{P}_y\big(N_x^+ = n+1, \mathcal{T}_x^{+,n+1} < \infty\big) \\ \\
&= \mathbb{P}_y\big(\mathcal{T}_x^{+,n+2} - \mathcal{T}_x^{+,n+1} = \infty, \mathcal{T}_x^{+,n+1} < \infty\big) \\ \\
&= \mathbb{P}_y\big(\mathcal{T}_x^{+,n+1} < \infty\big) \mathbb{P}_y\big(\mathcal{T}_x^{+,n+2} - \mathcal{T}_x^{+,n+1} = \infty \;\big|\; \mathcal{T}_x^{+,n+1} < \infty\big) \\ \\
&\overset{\text{Prop. Forte}}{=} \mathbb{P}_y\big(\mathcal{T}_x^{+,n+1} < \infty\big) \mathbb{P}_x(\mathcal{T}_x^+ = \infty) \\ \\
&= \mathbb{P}_y(N_x^+ > n)(1 - \rho_{xx})
\end{aligned}$$

---

### Teorema 3:

Sejam $x$ e $y$ estados que se comunicam, então ambos estados são **recorrentes** ou **transientes**.

### Corolário:

Em uma cadeia irredutível todos os estados são **recorrentes** ou **transientes**.

> $$\hookrightarrow \text{Propriedade da Cadeia.}$$