# Aula 18

**Data:** 27/04/2026

## Revisão: Reversibilidade

**$Def.:$** Uma distribuição de probabilidade $\pi$ em $\mathcal{X}$ satisfaz a **Condição de Balanceamento Detalhado (CBD)** se:

$$\pi(x)P(x,y) = \pi(y)P(y,x) \quad \forall x, y \in \mathcal{X}$$

Onde $P$ é a Matriz de Transição.

**$Prop.:$** $\pi$ satisfaz CBD $\Rightarrow \pi$ é distribuição estacionária.

**Prova:**$\quad \pi P(y) = \sum_{x \in \mathcal{X}} \pi(x)P(x,y) = \sum_{x \in \mathcal{X}} \pi(y)P(y,x) = \pi(y), \quad \forall x, y \in \mathcal{X}$

---

**Observação:** Se $\pi$ satisfaz CBD e $X_0 \sim \pi$, então

$$\mathbb{P}_{\pi} (X_0=x_0, X_1=x_1, \dots, X_t=x_t)$$

$$= \mathbb{P}_{\pi} (X_0=x_0) \prod_{s=1}^{t} \mathbb{P}_{\pi} (X_s=x_s \mid X_{s-1}=x_{s-1}, \dots, X_0=x_0)$$

$$= \mathbb{P}_{\pi} (X_0=x_0) \prod_{s=1}^{t} \mathbb{P}_{\pi} (X_s=x_s \mid X_{s-1}=x_{s-1})$$

$$= \pi(x_0) \prod_{s=1}^{t} P(x_{s-1}, x_s)$$

$$= \pi(x_0) P(x_0, x_1) P(x_1, x_2) \dots P(x_{t-1}, x_t)$$

$$\xrightarrow{CBD} = \pi(x_1) P(x_1, x_0) P(x_1, x_2) \dots P(x_{t-1}, x_t)$$

$$= P(x_1, x_0) \pi(x_2) P(x_2, x_1) P(x_2, x_3) \dots P(x_{t-1}, x_t)$$

$$= \text{ITERANDO} = P(x_1, x_0) P(x_2, x_1) P(x_3, x_2) \dots P(x_t, x_{t-1}) \pi(x_t)$$

$$= \pi(x_t) P(x_t, x_{t-1}) P(x_{t-1}, x_{t-2}) \dots P(x_1, x_0)$$

$$= \mathbb{P}_{\pi} (X_0=x_t, X_1=x_{t-1}, \dots, X_t=x_0)$$

Em particular, temos "ao inverter o tempo", a cadeia tem a mesma lei.

---

## Exemplos de Cadeias Reversíveis

### 1. P.A. em Hipercubo
P.A. em $\mathcal{X} = \{0,1\}^n$

$$P(x,y) = \begin{cases} \frac{1}{n} , & \text{se } d_H(x,y)=1 \\ 0 , & \text{c.c.} \end{cases}$$

$\pi(x) = \frac{1}{2^n} , \forall x \in \mathcal{X}$ é a dist. estacionária.

onde $d_H(x,y) = \sum_{i=1}^n \mathbb{1}_{\{x_i \neq y_i\}}$ (Distância de Hamming)

$\pi$ satisfaz CBD, pois $\forall x \in \mathcal{X}$

$$\pi(x) P(x,y) = \frac{1}{2^n} \begin{cases} 0 & \text{se } d_H(x,y) > 1 \\ \frac{1}{n} & \text{se } d_H(x,y) = 1 \end{cases}$$

$$\pi(y) P(y,x) = \frac{1}{2^n} \begin{cases} 0 & \text{se } d_H(x,y) > 1 \\ \frac{1}{n} & \text{se } d_H(x,y) = 1 \end{cases}$$

Para todo $y \in \mathcal{X}$.

---

### 2. Cadeia de Ehrenfest
Considere $n \geq 2$ bolas numeradas de 1 a $n$, em duas urnas $A$ e $B$.

Em cada etapa, sorteamos uma bola uniformemente ao acaso e a trocamos de urna. Denote $X_t$ o número de bolas na urna $A$ após $t$ sorteios, com $X_0$ sendo o número de bolas inicialmente alocado a urna $A$.

**AF.1** $(X_t)_{t \geq 0}$ é uma C.M. em $\mathcal{X} = \{0, 1, \dots, n\}$ com matriz de transição:

$$P(x,y) = \begin{cases} \frac{(n-x)}{n} , & \text{se } x \in \{1, \dots, n-1\} \text{ e } y = x+1 \\ \frac{x}{n} , & \text{se } x \in \{1, \dots, n-1\} \text{ e } y = x-1 \\ 0 , & \text{se } x \in \{1, \dots, n-1\} \text{ e } y \neq \{x-1, x+1\} \\ 1 , & \text{se } (x,y) \in \{(0,1), \dots, (n, n-1)\} \end{cases}$$

**AF.2** $\pi \sim Bin(n, \frac{1}{2})$ satisfaz CBD.

**Prova:** Queremos mostrar que $\pi(x) P(x,y) = \pi(y) P(y,x)$

$$\iff \binom{n}{x} \left(\frac{1}{2}\right)^n P(x,y) = \binom{n}{y} \left(\frac{1}{2}\right)^n P(y,x)$$

Para todos $x, y \in \mathcal{X}$.

**Fixa $x=0$:**

$$\binom{n}{0} P(0,y) = \binom{n}{y} P(y,0) \quad \forall y \in \{0, \dots, n\}$$

tomando $y=1$, temos

$$\binom{n}{0} = \binom{n}{1} P(1,0) = \binom{n}{1} \frac{1}{n} = 1 \quad \checkmark$$

Para $y \neq \{0, 1\}$, a condição vale automaticamente.

**Fixa $x=n$ e observe que**
para $y \neq n-1$, $P(n,y)=0$ e $P(y,n)=0$
$\Rightarrow$ Condição CBD vale para todos os pares $(n,y)$ com $y \neq n-1$.

**Para $y=n-1$:**

$1 = \binom{n}{n} P(n, n-1) = \binom{n}{n-1} P(n-1, n) = \binom{n}{n-1} \cdot \frac{1}{n} = 1 \quad \checkmark$

**Fixa $x \in \{1, \dots, n-1\}$ e note**
Precisamos verificar a CBD apenas para $y=x-1$ e $y=x+1$.

**Para $y=x+1$:**

$$\underbrace{\binom{n}{x} \frac{(n-x)}{n}}_{\frac{n!}{(n-x)! x!} \cdot \frac{(n-x)}{n}} = \underbrace{\binom{n}{x+1} \frac{(x+1)}{n}}_{\frac{n!}{(n-(x+1))! (x+1)!} \cdot \frac{(x+1)}{n}}$$

$$\frac{n!}{(n-x-1)! x! \cdot n} = \frac{n!}{(n-x-1)! x! \cdot n}$$

**Para $y=x-1$, podemos verificar de maneira similar!**

---

### 3. Cadeias de Nascimentos e Mortes
$\mathcal{X} \in \{0, 1, \dots, n\}$
$P(x,y) = 0$ se $|x-y| > 1$

Além disso,
$P(x, x+1) = p_x > 0, \forall 0 < x \leq n-1$

$P(x, x-1) = q_x > 0, \forall 1 \leq x \leq n$

$P(x,x) = 1 - p_x - q_x = r_x \in [0, 1), \forall 1 \leq x \leq n$

$P(0,0) = 1 - p_0 = r_0 \in [0, 1]$

$P(n,n) = 1 - q_n = r_n \in [0, 1]$

Pode-se verificar que vale a CBD para

$$\pi(x) = \pi(0) \prod_{y=1}^x \left( \frac{p_{y-1}}{q_y} \right), \quad 1 \leq x \leq n$$

*(Nota: $\pi$ é a única dist. est.)*

onde

$$\pi(0) = \left( 1 + \sum_{x=1}^n \prod_{y=1}^x \left( \frac{p_{y-1}}{q_y} \right) \right)^{-1}$$