# Aula 12

**Data:** 06/04/2026

## Revisão: Tempo de Parada e Propriedade Forte de Markov

* **Tempo de Parada $\tau$**: Uma V.A. [cite_start]é um tempo de parada se o evento $\{\tau = t\}$ só depende de $X_0, \dots, X_t$[cite: 162, 165].
* [cite_start]Matematicamente: $\{\tau = t\} = \{X_0 \in B_0, X_1 \in B_1, \dots, X_t \in B_t\}$ para $B_0, B_1, \dots, B_t \in \mathcal{X}$[cite: 164].
* [cite_start]Um evento $A$ depende de $\tau$ de modo que $A \cap \{\tau = t\}$ só depende de $X_0, \dots, X_t$[cite: 166, 167].

### [cite_start]Propriedade Forte de Markov [cite: 174]
[cite_start]Para todo tempo de parada $\tau$, estados $x, x_1, \dots, x_m \in \mathcal{X}$ e evento $A$ como definido acima[cite: 176]:
[cite_start]$$P(X_{\tau+1}=x_1, \dots, X_{\tau+m}=x_m | \tau=t, X_\tau=x, A) = P_x(X_1=x_1, \dots, X_m=x_m)$$ [cite: 176]

---

## [cite_start]Ruína do Jogador [cite: 179]

[cite_start]Considere o passeio aleatório em $\{0, \dots, N\}$ com estados absorventes em $0$ e $N$[cite: 178, 180, 186].
* [cite_start]$\tau_0 = \min\{t \ge 0 : X_t = 0\}$[cite: 187].
* [cite_start]$\tau_N = \min\{t \ge 0 : X_t = N\}$[cite: 188].

### 1. Probabilidade de Ruína ($P_k$)
[cite_start]Seja $P_k = P_k(\tau_N < \tau_0)$ a probabilidade de atingir $N$ antes de $0$ saindo de $k$[cite: 190, 191].
* [cite_start]Pela análise do primeiro passo: $P_k = p P_{k+1} + (1-p) P_{k-1}$ para $1 \le k \le N-1$[cite: 194, 195].
* [cite_start]Condições de contorno: $P_0 = 0$ e $P_N = 1$[cite: 196].

#### Resolução por Diferenças
[cite_start]Defina $\Delta_k = P_{k+1} - P_k$[cite: 201].
* [cite_start]$\Delta_k = \frac{(1-p)}{p} \Delta_{k-1} = \left(\frac{1-p}{p}\right)^k \Delta_0$[cite: 206].
* [cite_start]Como $\sum_{k=0}^{N-1} \Delta_k = P_N - P_0 = 1$[cite: 210, 211]:
    * [cite_start]**Se $p = 1/2$**: $\Delta_0 = 1/N$ [cite: 220][cite_start], logo $P_k = k/N$[cite: 224].
    * [cite_start]**Se $p \ne 1/2$**: $P_k = \frac{(\frac{1-p}{p})^k - 1}{(\frac{1-p}{p})^N - 1}$[cite: 226].

---

### [cite_start]2. Esperança do Tempo de Absorção ($f_k$) [cite: 235]
[cite_start]Calcular $f_k = E_k[\tau]$, onde $\tau = \tau_{\{0,N\}}$[cite: 235].
* [cite_start]Condições de contorno: $f_0 = 0$ e $f_N = 0$[cite: 236].
* [cite_start]Recursão: $f_k = 1 + p f_{k+1} + (1-p) f_{k-1}$[cite: 261].
* [cite_start]Também expressa como: $f_k = p(1 + f_{k+1}) + (1-p)(1 + f_{k-1})$[cite: 261].

#### [cite_start]Caso $p = 1/2$ [cite: 264]
[cite_start]Defina $\Delta_k = f_{k+1} - f_k$[cite: 263].
* [cite_start]$\Delta_k = \Delta_{k-1} - 2$, ou $\Delta_{k-1} = \Delta_k + 2$[cite: 268].
* [cite_start]Usando a soma telescópica $\sum_{k=0}^{N-1} \Delta_k = f_N - f_0 = 0$[cite: 272].
* [cite_start]Resolvendo o sistema: $\Delta_N = -(N+1)$[cite: 276].
* [cite_start]**Resultado Final**: $f_k = k(N-k)$[cite: 159].