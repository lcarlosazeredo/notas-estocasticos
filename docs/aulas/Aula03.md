# Aula 3: Processos Estocásticos

**Data:** 13/03/2026

## 📅 Datas de Provas
* **P1:** 06 de Maio
* **P2:** 26 de Junho
* **PF:** 03 de Julho
* **2CH:** 08 de Julho

---

## 1. Revisão
Cadeia de Markov e matriz de transição com 2 estados ($\mathcal{X} = \{0, 1\}$):
$$P = \begin{pmatrix} 1-p & p \\ q & 1-q \end{pmatrix}$$

Definimos $\mu_t = (\mu_t(0), \mu_t(1))$ para $t \ge 0$, com $\mu_t(x) = \mathbb{P}(X_t = x)$.
Vimos que:
$$\mu_t = \mu_0 P^t$$
Para provar esta relação, usamos que $\mu_t = \mu_{t-1} P$.

Assumindo que existe o limite:
* $\lim_{t \to \infty} \mu_t(0) = \pi(0)$
* $\lim_{t \to \infty} \mu_t(1) = \pi(1)$

Deduzimos o sistema:
$$\begin{cases} \pi(0) = \pi(0)(1-p) + \pi(1)q \\ \pi(1) = \pi(0)p + \pi(1)(1-q) \end{cases} \iff \pi = \pi P$$
Além disso, temos a condição para vetor de probabilidade: $\pi(0) + \pi(1) = 1$.

---

## 2. Distribuição Estacionária
Resolvendo o sistema anterior, encontramos:
$$\pi(0) = \frac{q}{p+q} \quad \text{e} \quad \pi(1) = \frac{p}{p+q}$$

**Definição:** Qualquer vetor de probabilidade $v$ tal que $v = v P$ é chamado de **medida estacionária** ou **invariante** para a cadeia.

### Exemplos:
1.  **Se $p = q \neq 0$:** $\pi(0) = \pi(1) = \frac{1}{2}$.
2.  **Se $p = q = 0$:** A matriz é a identidade ($P = I$). Para qualquer $\mu_0$, temos $\mu_t = \mu_0 P^t = \mu_0 I = \mu_0$. Logo, $\pi = \lim_{t \to \infty} \mu_t = \mu_0$.

---

## 3. Simulação de uma C.M. com 2 Estados
Como simular no computador dada a matriz $P$?

**Algoritmo:**
1.  Inicializa $X_0$ com uma certa distribuição $\mu$.
2.  Para $t \ge 1$, gera uma variável uniforme $U_t \sim \text{Unif}[0, 1]$ independente de tudo o resto.
3.  Se $X_{t-1} = 0$, define:
    $$X_t = \begin{cases} 1 & \text{se } U_t \le p \\ 0 & \text{caso contrário} \end{cases}$$
4.  Se $X_{t-1} = 1$, define:
    $$X_t = \begin{cases} 0 & \text{se } U_t \le q \\ 1 & \text{caso contrário} \end{cases}$$

Este algoritmo pode ser representado por $X_t = F(X_{t-1}, U_t)$.

---

## 4. Velocidade de Convergência
Seja $\pi = (\pi(0), \pi(1)) = \left(\frac{q}{p+q}, \frac{p}{p+q}\right)$. Definimos o erro no tempo $t$ como:
$$\Delta_t = \mu_t(0) - \pi(0)$$

Desenvolvendo a expressão:
$$\Delta_t = \mu_{t-1}(0)(1-p) + \mu_{t-1}(1)q - \pi(0)$$
$$\Delta_t = \mu_{t-1}(0)(1-p) + (1 - \mu_{t-1}(0))q - \pi(0)$$
$$\Delta_t = \mu_{t-1}(0)(1 - p - q) + q - \pi(0)$$

Como $q = \pi(0)(p+q)$, chegamos a:
$$\Delta_t = \Delta_{t-1}(1 - (p+q))$$
Iterando o processo:
$$\Delta_t = \Delta_0 (1 - (p+q))^t$$