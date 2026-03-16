# Aula 2

**Data:** 11/03

$Def.:$ Seja $(\Omega, \mathcal{F}, \mathbb{P})$ um espaço de probabilidade.
Dizemos que a seq. $(X_t)_{t \ge 0}$ de V.A.'s assumindo valores em $\mathcal{X}$ é uma Cadeia de Markov, se:

$$\mathbb{P}(X_{t+1}=y \mid X_t=x, X_{t-1}=x_{t-1}, \dots, X_0=x_0) = \mathbb{P}(X_{t+1}=y \mid X_t=x) =: P_t(x,y)$$

$\forall x_{0}, \dots, x_{t-1}, x, y \in \mathcal{X}$ e $t \ge 0$ tais que:
$\mathbb{P}(X_{0}=x_{0}, \dots, X_{t-1}=x_{t-1}, X_{t}=x) > 0$

i.e., se vale a **Propriedade de Markov**.

A cadeia é dita **Homogênea no tempo** se $P_t(x,y)$ não depende de $t$.  
Vamos nos concentrar no caso homogêneo, onde $P_t(x,y) = P_1(x,y) = P(x,y)$.

---

## 1. Matriz de Transição ($P$)

Coletamos as probabilidades de transição em uma matriz $P = (P(x,y))$.  
**Propriedades (Matriz Estocástica):**

1. $P(x,y) \ge 0, \quad \forall x,y \in \mathcal{X}$.
2. A soma de cada linha é igual a 1, $\forall x \in \mathcal{X}$:  
$\sum_{y \in \mathcal{X}} P(x,y) = \sum_{y \in \mathcal{X}} \mathbb{P}(X_1 = y \mid X_0 = x) = \mathbb{P}(X_1 \in \mathcal{X} \mid X_0 = x) = 1$  
*Isso ocorre pois $\mathcal{X} = \bigcup_{y \in \mathcal{X}} \{y\}$ (o espaço de estados completo).*

> **Conclusão:** Uma matriz $P$ com essas propriedades é chamada de **Matriz Estocástica** e ela representa a transição de estados de uma Cadeia de Markov.

## 2. Distribuição Inicial ($\mu$)

A distribuição de $X_0$ é chamada de **distribuição inicial**:    
$&emsp;&emsp;&emsp;&emsp;\mu(x) = \mathbb{P}(X_0 = x), \quad x \in \mathcal{X}$      

<u>Notação:</u> $\mu = (\mu(x))_{x \in \mathcal{X}}$.  
Note que $\mu(x) \ge 0$ e $\sum_{x \in \mathcal{X}} \mu(x) = 1, \quad \forall x \in \mathcal{X}$.

### Exemplo: Eugene Onegin
* **Espaço de Estados:** $\mathcal{X} = \{\text{"Vogal"}, \text{"Consoante"}\}$  
* **Codificação:** - "Vogal" $\longleftrightarrow 0$  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;- "Consoante" $\longleftrightarrow 1$  
$\quad P = \begin{pmatrix} P(0,0) & P(0,1) \\ P(1,0) & P(1,1) \end{pmatrix} = \begin{pmatrix} 1-p & p \\ q & 1-q \end{pmatrix}$

* Dados do exemplo:- $1-p = 0,128 \implies p = 0,872$  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; - $q = 0,663 \implies 1-q = 0,337$
    
---

## 3. Perguntas Frequentes

1. Qual o comportamento assintótico da cadeia?  
Em outras palavras, se definimos $\mu_t = (\mu_{t}(0), \mu_{t}(1)) = (\mathbb{P}(X_t=0), \mathbb{P}(X_t=1))$  
Como $\mu_t$ se comporta para $t$ grande?
2. Como a distribuição inicial $\mu_0 = \mu = (\mu(0), \mu(1))$ <u>afeta</u> o comportamento da cadeia?
3. Ao observar os $n+1$ passos da cadeia, $X_0, X_1, \dots, X_n$, como podemos estimar a matriz de transição $P$?
4. Como simular no computador uma Cadeia de Markov?

---

## 4. Evolução da Distribuição ($\mu_t$)

Queremos saber qual a probabilidade da cadeia estar em um estado específico no tempo $t$, ou seja, $\mu_t(x) = \mathbb{P}(X_t = x)$. Tomemos $x=0$:

<u>Para o tempo $t=0$:</u> $\qquad \mu_t(0) = \mu_0(0) = \mu(0)$

<u>Para o tempo $t=1$:</u>

$$
\begin{aligned}
\mu_1(0) &= \mathbb{P}(X_1=0)\\
&= \mathbb{P}(X_0=0, X_1=0) + \mathbb{P}(X_0=1, X_1=0)\\      
&= \mathbb{P}(X_0=0)\mathbb{P}(X_1=0 \mid X_0=0) + \mathbb{P}(X_0=1)\mathbb{P}(X_1=0 \mid X_0=1)\\    
&= \mu_0(0)P(0,0) + \mu_0(1)P(1,0)
\end{aligned}
$$

Note que o termo acima é a primeira entrada da multiplicação vetor-matriz:

$$(\mu_0(0), \mu_0(1)) \begin{pmatrix} P(0,0) & P(0,1) \\ P(1,0) & P(1,1) \end{pmatrix}$$

Logo, de forma geral:
  
$$\mu_1 = \mu_0 P$$

---

<u>Para o tempo $t=2$:</u>

$$
\begin{aligned}
\mu_2(0) &= \mathbb{P}(X_2=0) \\
&= \mathbb{P}(X_1=0, X_2=0) + \mathbb{P}(X_1=1, X_2=0) \\
&= \mathbb{P}(X_1=0)\mathbb{P}(X_2=0 \mid X_1=0) + \mathbb{P}(X_1=1)\mathbb{P}(X_2=0 \mid X_1=1) \\
&= \mu_1(0)P(0,0) + \mu_1(1)P(1,0)
\end{aligned}
$$

Substituindo o resultado anterior ($\mu_1 = \mu_0 P$):

$$\mu_2 = \mu_1 P = (\mu_0 P) P = \mu_0 P^2$$

---

Iterando o argumento, podemos mostrar que:

&emsp;$\mu_t = \mu_0 P^t$, para todo $t \ge 0$, com a condição $P^0 = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix}$

---

## 5. Identificando a Distribuição Estacionária ($\pi$)

Supondo que existe

$$\lim_{t \to \infty} \mu_t(0) = \pi(0)$$

$$\implies \lim_{t \to \infty} \mu_t(1) = \lim_{t \to \infty} (1 - \mu_t(0)) = 1 - \lim_{t \to \infty} \mu_t(0) = 1 - \pi(0) := \pi(1)$$

---

Como identificar $(\pi(0), \pi(1)) = \pi$?

$$
\begin{cases} 
\mu_t(0) = \mu_{t-1}(0) P(0,0) + \mu_{t-1}(1) P(1,0) = \mu_{t-1}(0) (1-p) + \mu_{t-1}(1) q\\ 
\mu_t(1) = \mu_{t-1}(0) P(0,1) + \mu_{t-1}(1) P(1,1) = \mu_{t-1}(0) p + \mu_{t-1}(1) (1-q)
\end{cases}
$$

---

Tomando $t \to \infty$:

$$
\begin{cases} 
\pi(0) = \pi(0) (1-p) + \pi(1) q \\ 
\pi(1) = \pi(0) p + \pi(1) (1-q) 
\end{cases}
$$

**$\pi(0) + \pi(1) = 1$**.