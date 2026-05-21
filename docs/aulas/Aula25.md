# Aula 25

**Data:** 18/05/2026

## Processos Pontuais

Sejam $0 = l_0 < l_1 < l_2 < \dots < l_i < l_{i+1} < \dots$ uma sequência de números.

Defina:

$$A_i = [l_{i-1}, l_i), i \ge 1$$

$$|A_i| = l_i - l_{i-1}$$

Fixe $\lambda > 0$

Para cada $i \ge 1$, escolha $Y_i \sim \text{Poi}(\lambda |A_i|)$, que representa a quantidade de pontos a ser colocada em $A_i$, independentemente dos demais intervalos. 

Além disso, considere uma família $\{U_{i,j} , j = 1, 2, \dots\}$, de variáveis independentes e uniformemente distribuídas em $A_i$.

Dado o valor de $Y_i$, considere o conjunto aleatório:

$$\mathcal{S}_i = \begin{cases} 
\{U_{i,j} : j = 1, 2, \dots, Y_i\} & \text{se } Y_i \ge 1 \\ 
\emptyset & \text{se } Y_i = 0 
\end{cases}$$

Finalmente, defina $S = \bigcup_{i=1}^{\infty} S_i$ e ordene os pontos na sequência:

$$\mathcal{S}_1 = \min\{ s \ge 0 : s \in \mathcal{S} \}$$

$$\mathcal{S}_2 = \min\{ s > \mathcal{S}_1 : s \in \mathcal{S} \}$$

$$\mathcal{S}_k = \min\{ s > \mathcal{S}_{k-1} : s \in \mathcal{S} \}$$

Para cada conjunto $A \subset [0, \infty)$, defina:

$$N_{\mathcal{S}}(A) = \sum_{n=1}^{\infty} \mathbb{1}_{\{\mathcal{S}_n \in A\}}$$

> $\hookrightarrow$ Número de pontos de $\mathcal{S}$ que pertencem ao conjunto $A$.

O **Processo de Poisson** é determinado pela família de variáveis $\{ N(A), A \subset [0, \infty) \}$.

---

### Espaço Amostral do Processo de Poisson

$$\mathcal{M} = \left\{ s = (\mathcal{s}_n)_{n \ge 1} \subset [0, \infty) : \mathcal{s}_1 < \mathcal{s}_2 < \mathcal{s}_3 < \dots \text{ e  t.q. } N_s(A) < \infty, \, \text{ para todo intervalo } A \subset [0, \infty) \right\}$$

Defina $\mathcal{A}$ como a coleção de eventos de $\mathcal{M}$ da seguinte forma:

$$\mathcal{A} = \left\{ s \in \mathcal{M} : N_s(B_1) = b_1, \dots, N_s(B_l) = b_l \right\}$$

onde $l \ge 1$ e $B_1, \dots, B_l$ são intervalos 

#### Teorema 1:
Uma medida de probabilidade em $\mathcal{M}$ é completamente caracterizada pelas probabilidades dos eventos na coleção $\mathcal{A}$.

---

### Propriedades

Fixado um intervalo $B \subset [0, \infty)$, qual é a distribuição de $N(B)$?

* **P1:** $N(B) \sim \text{Poi}(\lambda |B|)$
* **P2:** Para cada escolha de $B_1, \dots, B_L$ de intervalos disjuntos, as variáveis $N(B_1), \dots, N(B_L)$ são independentes com $N(B_i) \sim \text{Poi}(\lambda |B_i|)$.
* **P3:** A distribuição condicional dos pontos em $S \cap B$ dado que $N(B) = n$ é a mesma de $n$ variáveis aleatórias uniformemente distribuídas em $B$.

---

* **P4 (Propriedade de Markov):**
    Seja $T \sim \text{Exp}(\lambda)$ independente do Processo de Poisson $\mathcal{S}$ em $[0, \infty)$. Definimos $N(B)$:
    
    $$N(B) = \sum_{n=1}^{\infty} \mathbb{1}_{\{\mathcal{S}_n \in B\}} = \mathbb{1}_{\{T \in B\}} + \tilde{N}(B - T)$$
    
    onde:
    
    $$\mathcal{S}_n = \begin{cases} 
    T & \text{se } n = 1 \\ 
    \tilde{S}_{n-1} + T & \text{se } n \ge 2 
    \end{cases}$$

    O processo $N$ é um processo de Poisson de parâmetro $\lambda$.

* **P5:** $T_1 = \mathcal{S}_1$, $T_2 = \mathcal{S}_2 - \mathcal{S}_1, \dots, T_k = \mathcal{S}_k - \mathcal{S}_{k-1}$ são v.a. i.i.d. com distribuição comum $\text{Exp}(\lambda)$.

> $\hookrightarrow$ A propriedade **P5** sugere uma construção alternativa para o Processo de Poisson: Gere v.a.s $T_1, T_2, T_3, \dots, T_k, \dots $ independentes com distribuição Exponencial e defina $\mathcal{S}_1 = T_1, \mathcal{S}_k = \mathcal{S}_{k-1} + T_k, k \ge 2$.

---

### Prova da Propriedade P1:

Queremos calcular $\mathbb{P}(N(B \cap A_i) = k)$. Sabendo que $A_i$ são os intervalos da partição:

$$\begin{aligned}
\mathbb{P}(N(B \cap A_i) = k) &= \sum_{h=k}^{\infty} \mathbb{P}(N(B \cap A_i) = k \mid Y_i = h) \mathbb{P}(Y_i = h) \\ \\
&= \sum_{h=k}^{\infty} \mathbb{P}\left( \sum_{j=1}^h \mathbb{1}_{\{U_{i,j} \in B \cap A_i\}} = k \right) \mathbb{P}(Y_i = h)
\end{aligned}$$

Como as variáveis $U_{i,j}$ são uniformes em $A_i$, a probabilidade de um ponto cair em $B \cap A_i$ é dada por $\frac{|B \cap A_i|}{|A_i|}$. Logo, a soma das indicadoras segue uma distribuição Binomial $\text{Bin}\left(h, \frac{|B \cap A_i|}{|A_i|}\right)$:

$$\begin{aligned}
&= \sum_{h=k}^{\infty} e^{-\lambda |A_i|} \frac{(\lambda |A_i|)^h}{h!} \cdot \binom{h}{k} \left( \frac{|B \cap A_i|}{|A_i|} \right)^k \left( 1 - \frac{|B \cap A_i|}{|A_i|} \right)^{h-k} \\ \\
&= \sum_{h=k}^{\infty} e^{-\lambda |A_i|} \frac{(\lambda |A_i|)^h}{h!} \cdot \frac{h!}{k!(h-k)!} \left( \frac{|B \cap A_i|}{|A_i|} \right)^k \left( \frac{|A_i| - |B \cap A_i|}{|A_i|} \right)^{h-k} \\ \\
&= \frac{\lambda^k |B \cap A_i|^k}{k!} e^{-\lambda |A_i|} \sum_{h=k}^{\infty} \frac{\lambda^{h-k} \left( |A_i| - |B \cap A_i| \right)^{h-k}}{(h-k)!}
\end{aligned}$$

Fazendo uma mudança de variável no somatório ($m = h - k$):

$$\begin{aligned}
&= \frac{(\lambda |B \cap A_i|)^k}{k!} e^{-\lambda |A_i|} \sum_{m=0}^{\infty} \frac{\left[ \lambda (|A_i| - |B \cap A_i|) \right]^m}{m!} \\ \\
&= \frac{(\lambda |B \cap A_i|)^k}{k!} e^{-\lambda |A_i|} \cdot e^{\lambda(|A_i|)} - |B \cap A_i| \\ \\
&= \frac{e^{-\lambda |B \cap A_i|} (\lambda |B \cap A_i|)^k}{k!}
\end{aligned}$$

$$\Rightarrow N(B \cap A_i) \sim \text{Poi}(\lambda |B \cap A_i|)$$