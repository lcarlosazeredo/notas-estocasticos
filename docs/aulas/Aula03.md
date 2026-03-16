# Aula 3

**Data:** 13/03/2026

## 📅 Datas de Provas
* **P1:** 06 de Maio
* **P2:** 26 de Junho
* **PF:** 03 de Julho
* **2CH:** 08 de Julho

---

## 1. Revisão
$(X_t)_{t \ge 0}$ Cadeia de Markov com 2 estados ($\mathcal{X} = \{0, 1\}$) e matriz de transição  

$$P = \begin{pmatrix} 1-p & p \\ q & 1-q \end{pmatrix}$$

Definimos $\mu_t = (\mu_t(0), \mu_t(1))$ para $t \ge 0$, com $\mu_t(x) = \mathbb{P}(X_t = x)$, $x \in \mathcal{X}$.

Vimos que:$\quad \mu_t = \mu_0 P^t$

Para provar esta relação, usamos que $\mu_t = \mu_{t-1} P, \forall t \ge 1$

Assumindo que existe

* $\lim_{t \to \infty} \mu_t(0) = \pi(0)$

* $\lim_{t \to \infty} \mu_t(1) = \pi(1)$

Deduzimos o sistema:

$$\begin{cases} \pi(0) = \pi(0)(1-p) + \pi(1)q \\ \pi(1) = \pi(0)p + \pi(1)(1-q) \end{cases} \iff \pi = \pi P$$

Além disso,

$\pi(0) + \pi(1) = \lim_{t \to \infty} \mu_t(0)  + \lim_{t \to \infty} \mu_t(1)  =  \lim_{t \to \infty}(\mu_t(0) + \mu_t(1))   =  1$.

---

## 2. Distribuição Estacionária
Resolvendo o sistema anterior, encontramos:

$$\pi(0) = \frac{q}{p+q} \quad \text{e} \quad \pi(1) = \frac{p}{p+q}$$

$Def:$ Qualquer vetor de probabilidade $v$ tal que $v = v P$ é chamado de **medida estacionária** ou **invariante** para a cadeia.

Exemplos:

1.  **Se $p = q \neq 0$:** $\pi(0) = \pi(1) = \frac{1}{2}$.
2.  **Se $p = q = 0$:** A matriz é a identidade ($P = I$).  
    Para qualquer $\mu_0$, temos $\mu_t = \mu_0 P^t = \mu_0 I = \mu_0$.  
    Logo, $\pi = \lim_{t \to \infty} \mu_t = \lim_{t \to \infty} \mu_0 = \mu_0$.

---

## 3. Simulação de uma C.M. com 2 Estados
Como simular uma C.M. com 2 estados e matriz $P$?

**Algoritmo:**  
1.  Inicializa $X_0$ com uma certa distribuição $\mu$.  
2.  Para $t \ge 1$, gera uma variável uniforme $U_t \sim \text{Unif}[0, 1]$ independente de tudo o resto. 
 
&emsp;Se $X_{t-1} = 0$, defina:  
&emsp;&emsp;&emsp;$X_t = \begin{cases} 1 & \text{se } U_t \le p \\ 0 & \text{caso contrário} \end{cases}$
     
&emsp;Se $X_{t-1} = 1$, defina:  
&emsp;&emsp;&emsp;$X_t = \begin{cases} 0 & \text{se } U_t \le q \\ 1 & \text{caso contrário} \end{cases}$

Obs.: Neste algoritmo representamos $X_t = F(X_{t-1}, U_t)$  
onde $F(X_{t-1}, U_t) = \begin{cases} 1 & \text{se }(x=1 \quad e \quad u \le 1-q) \text{ ou } (x=0 \quad e \quad  u \le p)\\ 0 & \text{c. c.} \end{cases}$

---
Por que o algoritmo funciona? (Verifica Matriz P)

Analisamos a probabilidade de transição condicionada a todo o histórico:

$$\mathbb{P}(X_{t+1}=1 \mid X_t=x, X_{t-1}=x_{t-1}, \dots, X_0=x_0)$$

Pela definição da função $F$:

$$= \mathbb{P}(F(X_t, U_{t+1})=1 \mid X_t=x, X_{t-1}=x_{t-1}, \dots, X_0=x_0)$$

Como $X_t = x$ é dado:

$$= \mathbb{P}(F(x, U_{t+1})=1 \mid X_t=x, \dots, X_0=x_0)$$

Como $U_{t+1}$ é independente do passado:

$$= \mathbb{P}(F(x, U_{t+1})=1) = 
\begin{cases} 
\mathbb{P}(U_{t+1} \le 1-q) = 1-q, & \text{se } x=1 \\ 
\mathbb{P}(U_{t+1} \le p) = p, & \text{se } x=0 
\end{cases}$$

De modo similar, podemos mostrar que:

$$\mathbb{P}(X_{t+1}=1 \mid X_t=x) = \mathbb{P}(F(x, U_{t+1})=1)$$

Confirmando que o algoritmo simula corretamente as probabilidades da matriz $P$.

---

## 4. Velocidade de Convergência para a Distribuição Estacionária

Lembre que para $p, q$ tais que $p, q > 0$.  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;$\mu_t = (\mu_t(0), \mu_t(1)), \quad \forall t \ge 0$  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;$\pi = (\pi(0), \pi(1)) = \left( \frac{q}{p+q}, \frac{p}{p+q} \right)$

E defina $\Delta_t$ como a diferença entre a distribuição no tempo $t$ e a distribuição estacionária:

$$\Delta_t = \mu_t(0) - \pi(0)$$

Note que

$$
\begin{aligned}
\Delta_t &= \mu_t(0) - \pi(0) \\
&= \mu_{t-1}(0)P(0,0) + \mu_{t-1}(1)P(1,0) - \pi(0)\\
&= \mu_{t-1}(0)(1-p) + \mu_{t-1}(1)q - \pi(0) \\
&= \mu_{t-1}(0)(1-p) + (1 - \mu_{t-1}(0))q - \pi(0) \\
&= \mu_{t-1}(0) - p\mu_{t-1}(0) + q - q\mu_{t-1}(0) - \pi(0) \\
&= [\mu_{t-1}(0) - \pi(0)] - (p+q)\mu_{t-1}(0) + q
\end{aligned}
$$

Como $\pi(0) = \frac{q}{p+q}$, temos que $q = (p+q)\pi(0)$. Substituindo:

$$
\begin{aligned}
\Delta_t &= \Delta_{t-1} - (p+q)\mu_{t-1}(0) + (p+q)\pi(0) \\
&= \Delta_{t-1} - (p+q)[\mu_{t-1}(0) - \pi(0)] \\
&= \Delta_{t-1} - (p+q)\Delta_{t-1} \\
&= \Delta_{t-1}(1 - (p+q))
\end{aligned}
$$

Iterando o argumento até o tempo inicial $t=0$:

$$\Delta_t = \Delta_0 (1 - (p+q))^t$$



!!! info "Simulação Interativa Disponível"
    [Acessar Simulador :material-open-in-new:](../simulacoes/markov_2state_simulation[6].html){: .md-button target="_blank" }