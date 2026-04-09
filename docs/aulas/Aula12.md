# Aula 12

**Data:** 06/04/2026

## Revisão

### Tempo de Parada
$\mathcal{T} \in \mathbb{N} \cup \{ \infty \}$ é um tempo de parada se, para todo $t \ge 0$: 

$$\{\mathcal{T} = t\} = \{X_0 \in B_0, X_1 \in B_1, \dots, X_t \in B_t\}$$ 

onde $B_0, B_1, \dots, B_t \in \mathcal{X}$. 

Ou seja, o evento $\{\mathcal{T} = t\}$ só depende de $X_0, \dots, X_t$. 


### Propriedade Forte de Markov
Para todo tempo de parada $\mathcal{T}$, estados $x, x_1, \dots, x_m \in \mathcal{X}$ e evento $A$: 

$$P(X_{\mathcal{T}+1} = x_1, \dots, X_{\mathcal{T}+m} = x_m | \mathcal{T} = t, X_\mathcal{T} = x, A) = \mathbb{P}_x(X_1 = x_1, X_2 = x_2, \dots, X_m = x_m)$$ 

onde $A$ depende de $\mathcal{T}$ de modo que $A \cap \{\mathcal{T} = t\}$ só depende de $X_0, \dots, X_t$. 

---

## Ruína do Jogador

Consideramos um passeio aleatório no espaço de estados $\{0, 1, \dots, N\}$, onde os estados $0$ e $N$ são barreiras absorventes. Definimos os tempos de parada como:

* $\mathcal{T}_{0} = \min \{t \ge 0 : X_t = 0\}$:
* $\mathcal{T}_N = \min \{t \ge 0 : X_t = N\}$:

**$p_k = \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0) = ?$**

**$\mathbb{E}_k[\min \{\mathcal{T}_0, \mathcal{T}_N\}] = ?$**


### 1. Probabilidade de Absorção ($p_k$)
O objetivo é encontrar $p_k = \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0)$, que representa a probabilidade de o processo atingir o estado $N$ antes do estado $0$, partindo de um estado inicial $k$.

Pela análise do primeiro passo e a propriedade de Markov:

$$p_k = \mathbb{P}_k(X_1 = k+1) \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 | X_1 = k+1) + \mathbb{P}_k(X_1 = k-1) \mathbb{P}_k(\mathcal{T}_N < \mathcal{T}_0 | X_1 = k-1)$$

$$= p \mathbb{P}_{k+1}(\mathcal{T}_N < \mathcal{T}_0) + (1-p) \mathbb{P}_{k-1}(\mathcal{T}_N < \mathcal{T}_0)$$

$$= p p_{k+1} + (1-p) p_{k-1}, \quad \forall \ 1 \le k \le N-1$$

* $p_0 = 0$.
* $p_N = 1$.

---

### 2. Resolução via Equações de Diferenças
Defina $\Delta_k = p_{k+1} - p_k$, $\quad 0 \le k \le N-1$.

E note que:

$$\Delta_k = p_{k+1} - (p p_{k+1} + (1-p) p_{k-1}) = (1-p)(p_{k+1} - p_{k-1}) = (1-p)(\Delta_k + \Delta_{k-1})$$

$$\implies \Delta_k(1 - (1-p)) = (1-p) \Delta_{k-1} \implies p \Delta_k = (1-p) \Delta_{k-1}$$

Obtemos a relação:

$$\Delta_k = \frac{1-p}{p} \Delta_{k-1} = \left( \frac{1-p}{p} \right)^k \Delta_0$$

Note também:

$$\sum_{k=0}^{N-1} \Delta_k = \Delta_0 + \Delta_1 + \dots + \Delta_{N-1} = p_N - p_0 = 1$$

Logo: $1 = \Delta_0 \sum_{k=0}^{N-1} \left( \frac{1-p}{p} \right)^k$

---

### 3. Resultados Gerais

#### Caso Simétrico ($p = 1/2$)
* $\Delta_0 = 1/N$.
* $\Delta_k = \Delta_0 = 1/N, \quad \forall \ 0 \le k \le N-1$.
* $p_k = \frac{k}{N}, \quad 0 \le k \le N$.
* A probabilidade de ruína é $\mathbb{P}_k(\mathcal{T}_0 < \mathcal{T}_N) = 1 - \frac{k}{N} = \frac{N-k}{N}$.

#### Caso Assimétrico ($p \neq 1/2$)
* $p_k = \frac{\left( \frac{1-p}{p} \right)^k - 1}{\left( \frac{1-p}{p} \right)^N - 1}$.

---

**Nota:** Para variáveis aleatórias discretas não negativas, a esperança pode ser escrita em termos de sua cauda: $\mathbb{E}[X] = \sum_{x=0}^{\infty} \mathbb{P}(X > x) = \sum_{x=1}^{\infty} \mathbb{P}(X \ge x)$. [Verifique]

---

### 4. Esperança do Tempo de Absorção ($f_k$)

[cite_start]**Objetivo:** Calcular $f_k = \mathbb{E}_k[\tau]$, onde $\tau = \tau_{\{0,N\}}$ é o tempo de absorção nos estados $\{0, N\}$[cite: 27].
[cite_start]Para os estados absorventes, temos as condições de contorno[cite: 27]:
* [cite_start]$f_0 = 0$ [cite: 27]
* [cite_start]$f_N = 0$ [cite: 27]

> [cite_start]**Exercício:** Verificar que para uma V.A. discreta não negativa $X$, a esperança pode ser escrita em termos de sua cauda[cite: 27]:
> [cite_start]$$\mathbb{E}[X] = \sum_{x=0}^{\infty} \mathbb{P}(X > x) = \sum_{x=1}^{\infty} \mathbb{P}(X \ge x)$$ [cite: 27]

[cite_start]Para $1 \le k \le N-1$[cite: 27]:
[cite_start]$$f_k = \mathbb{E}_k[\tau] = \sum_{t=0}^{\infty} \mathbb{P}_k(\tau > t) = \mathbb{P}_k(\tau > 0) + \sum_{t=1}^{\infty} \mathbb{P}_k(\tau > t)$$ [cite: 27]
[cite_start]Sabendo que $\mathbb{P}_k(\tau > 0) = 1$ [cite: 27][cite_start], analisamos para $t \ge 1$ usando a probabilidade total em relação ao primeiro passo[cite: 27]:
[cite_start]$$\mathbb{P}_k(\tau > t) = \mathbb{P}_k(X_1 = k-1)\mathbb{P}_k(E_t | X_1 = k-1) + \mathbb{P}_k(X_1 = k+1)\mathbb{P}_k(E_t | X_1 = k+1)$$ [cite: 27]
[cite_start]Onde $E_t$ representa o evento do processo não ser absorvido até o tempo $t$[cite: 27].

### Caso Particular: $k=1$
[cite_start]Para $t \ge 1$, e considerando que o estado $0$ é absorvente ($\mathbb{P}_1(E_t | X_1 = 0) = 0$)[cite: 28]:
[cite_start]$$\mathbb{P}_1(\tau > t) = p \mathbb{P}_1(X_2 \notin \{0,N\}, \dots, X_t \notin \{0,N\} | X_1 = 2)$$ [cite: 28]
[cite_start]Pela **Propriedade Forte de Markov**, isso se reduz a[cite: 28]:
[cite_start]$$\mathbb{P}_1(\tau > t) = p \mathbb{P}_2(\tau > t-1)$$ [cite: 28]

[cite_start]Assim, a esperança em $k=1$ resulta em[cite: 28]:
[cite_start]$$f_1 = 1 + p \mathbb{E}_2[\tau] = 1 + p f_2$$ [cite: 28]
[cite_start]Que também pode ser escrita como $f_1 = p(1 + f_2) + (1-p)(1 + f_0)$[cite: 28].

### Equação Geral de Recorrência
[cite_start]De modo geral, para $1 \le k \le N-1$[cite: 29]:
[cite_start]$$f_k = p(1 + f_{k+1}) + (1-p)(1 + f_{k-1}) = 1 + p f_{k+1} + (1-p) f_{k-1}$$ [cite: 29]

---

## Resolução para o Caso Simétrico ($p = 1/2$)

[cite_start]Definimos a diferença $\Delta_k = f_{k+1} - f_k$ para $0 \le k \le N-1$[cite: 29].
[cite_start]Substituindo $p = 1/2$ na equação geral[cite: 29]:
[cite_start]$$f_k = 1 + \frac{1}{2} f_{k+1} + \frac{1}{2} f_{k-1} \implies \Delta_k = \Delta_{k-1} - 2$$ [cite: 29]
[cite_start]Ou seja, $\Delta_{k-1} = \Delta_k + 2$[cite: 29].

### Soma Telescópica
[cite_start]Utilizando a propriedade da soma telescópica e as condições de contorno[cite: 30]:
[cite_start]$$\sum_{k=0}^{N-1} \Delta_k = f_N - f_0 = 0$$ [cite: 30]

[cite_start]Iterando as diferenças a partir de $\Delta_N$[cite: 30]:
* [cite_start]$\Delta_{N-1} = \Delta_N + 2$ [cite: 30]
* [cite_start]$\Delta_{N-2} = \Delta_N + 2 \cdot 2$ [cite: 30]
* [cite_start]$\Delta_k = \Delta_N + 2(N-k)$ [cite: 30]

[cite_start]Substituindo na soma[cite: 30]:
[cite_start]$$\sum_{k=0}^{N-1} (\Delta_N + 2(N-k)) = N \Delta_N + 2 \sum_{k=1}^{N} k = 0$$ [cite: 30]
[cite_start]$$N \Delta_N + 2 \frac{N(N+1)}{2} = N(\Delta_N + N + 1) = 0$$ [cite: 30]
[cite_start]$\implies \Delta_N = -(N+1)$[cite: 30].

[cite_start]**Resultado Final:** Através da integração das diferenças, obtemos $f_k = k(N-k)$[cite: 30].











---

xxx



---

### 2. Esperança do Tempo de Absorção ($f_k$)
[cite_start]**Objetivo:** Calcular $f_k = \mathbb{E}_k[\mathcal{T}]$, onde $\mathcal{T} = \mathcal{T}_{\{0,N\}}$. [cite: 27]
[cite_start]Sabemos que $f_0 = 0$ e $f_N = 0$. [cite: 27]

[cite_start]Para $1 \le k \le N-1$: [cite: 27]
[cite_start]$$f_k = \mathbb{E}_k[\mathcal{T}] = \sum_{t=0}^{\infty} \mathbb{P}_k(\mathcal{T} > t) = \mathbb{P}_k(\mathcal{T} > 0) + \sum_{t=1}^{\infty} \mathbb{P}_k(\mathcal{T} > t)$$ [cite: 27]
[cite_start]Pela análise do primeiro passo: [cite: 28, 29]
[cite_start]$$f_k = p(1 + f_{k+1}) + (1-p)(1 + f_{k-1}) = 1 + p f_{k+1} + (1-p) f_{k-1}$$ [cite: 29]

#### Caso $p = \frac{1}{2}$
[cite_start]Defina $\Delta_k = f_{k+1} - f_k$ para $0 \le k \le N-1$. [cite: 29]
[cite_start]$\implies \Delta_k = \Delta_{k-1} - 2 \iff \Delta_{k-1} = \Delta_k + 2$ [cite: 29]

[cite_start]Usando a soma telescópica $\sum_{k=0}^{N-1} \Delta_k = f_N - f_0 = 0$: [cite: 30]
[cite_start]$$N \Delta_N + 2 \frac{N(N+1)}{2} = 0 \implies \Delta_N = -(N+1)$$ [cite: 30]

[cite_start]Resultando na fórmula final: $f_k = k(N-k)$. [cite: 30]