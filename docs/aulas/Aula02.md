# Aula 2: Processos Estocásticos

**Data:** 11/03 [cite: 70]

Seja $(\Omega, \mathcal{F}, \mathbb{P})$ um espaço de probabilidade [cite: 70].
Dizemos que $(X_t)_{t \ge 0}$ é uma Cadeia de Markov se assume valores em um conjunto finito ou enumerável $X$ [cite: 70, 71]:

$$\mathbb{P}(X_{t+1}=y \mid X_t=x, X_{t-1}=x_{t-1}, \dots, X_0=x_0) = \mathbb{P}(X_{t+1}=y \mid X_t=x) =: P_t(x,y)$$

Esta é a **Propriedade de Markov** [cite: 71].

A cadeia é dita **Homogênea no tempo** se $P_t(x,y)$ não depende de $t$ [cite: 71]. Vamos nos concentrar no caso homogêneo, onde $P_t(x,y) = P_1(x,y) = P(x,y)$ [cite: 72].

---

## 1. Matriz de Transição ($P$)

Coletamos as probabilidades de transição em uma matriz $P = (P(x,y))$ [cite: 73].
**Propriedades (Matriz Estocástica):** [cite: 73]
1. $P(x,y) \ge 0, orall x,y \in X$.
2. $\sum_{y \in X} P(x,y) = 1, orall x \in X$ (pela lei da Probabilidade Total).

---

## 2. Distribuição Inicial ($\mu$)

A distribuição de $X_0$ é chamada de distribuição inicial [cite: 74]:
$$\mu(x) = \mathbb{P}(X_0 = x), \quad x \in X$$
Notação: $\mu = (\mu(x))_{x \in X}$ [cite: 74].
Note que $\mu(x) \ge 0$ e $\sum_{x \in X} \mu(x) = 1$ [cite: 74].

### Exemplo: Eugene Onegin
* **Espaço de estados:** $X = \{	ext{"Vogal"}, 	ext{"Consoante"}\}$ [cite: 74].
* **Codificação:** $	ext{Vogal} \mapsto 0$, $	ext{Consoante} \mapsto 1$ [cite: 74].
* **Matriz:** $P =  egin{pmatrix} 1-p & p \ q & 1-q \end{pmatrix}$ [cite: 74].
    * Onde $1-p = 0,128$ e $q = 0,663$ [cite: 74].

---

## 3. Perguntas Frequentes

1. Qual o comportamento assintótico da cadeia? (Como $\mu_t$ se comporta para $t$ grande) [cite: 75].
2. Como a distribuição inicial $\mu_0 = \mu$ afeta o comportamento da cadeia? [cite: 75].
3. Ao observar os passos $X_0, X_1, \dots, X_n$, como podemos estimar a matriz $P$? [cite: 76].
4. Como simular no computador uma Cadeia de Markov? [cite: 77].

---

## 4. Evolução da Distribuição ($\mu_t$)

Para o tempo $t=1$ [cite: 78]:
$$\mu_1(0) = \mathbb{P}(X_1=0) = \mathbb{P}(X_0=0, X_1=0) + \mathbb{P}(X_0=1, X_1=0)$$
$$\mu_1(0) = \mu(0)P(0,0) + \mu(1)P(1,0)$$
Isso implica em $\mu_1 = \mu_0 P$ [cite: 78].

Para o tempo $t=2$ [cite: 79]:
$$\mu_2(0) = \mu_1(0)P(0,0) + \mu_1(1)P(1,0)$$
$\mu_2 = \mu_1 P = (\mu_0 P) P = \mu_0 P^2$ [cite: 79].

**Iterando o argumento:** [cite: 79]
$$\mu_t = \mu_0 P^t, 	ext{ com } P^0 = I =  egin{pmatrix} 1 & 0 \ 0 & 1 \end{pmatrix}$$

---

## 5. Identificando a Distribuição Estacionária ($\pi$)

Supondo que existe o limite [cite: 80]:
$$\lim_{t 	o \infty} \mu_t(0) = \pi(0) \quad 	ext{e} \quad \lim_{t 	o \infty} \mu_t(1) = \pi(1) = 1 - \pi(0)$$

Tomando o limite nas equações [cite: 81]:
$$ egin{cases} \pi(0) = \pi(0)(1-p) + \pi(1)q \ \pi(1) = \pi(0)p + \pi(1)(1-q) \end{cases}$$
E a condição $\pi(0) + \pi(1) = 1$ [cite: 81].