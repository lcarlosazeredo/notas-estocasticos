# Aula 10

**Data:** 30/03/2026

## Revisão: Passeio Aleatório Preguiçoso no Anel
* **Propriedades**: A cadeia é Irredutível e Aperiódica.
* **Distribuição Estacionária**: $\pi = (\pi(0), \dots, \pi(N-1)) = (\frac{1}{N}, \dots, \frac{1}{N})$ é a única distribuição estacionária.

### Objetivo
Demonstrar que o tempo de mistura $t_{mix}$ satisfaz:

$$t_{mix} = \min \left\{ t \ge 0 : \max_{x \in \{0, \dots, N-1\}} \| P^t(x, \cdot) - \pi \|_{VT} \le \frac{1}{4} \right\} \le N^2$$

### Observações
1. $t_{mix} > \frac{N^2}{32}$ (Ver pág. 64 do livro *Markov Chains and Mixing Times*, Yuval Peres e David A. Levin).
2. $\| P^t(x, \cdot) - \pi \|_{VT}$

&emsp;Utilizando a propriedade de que $\pi$ é invariante ($\pi = \pi P^t$):

$$\| P^t(x, \cdot) - \pi \|_{VT} = \| P^t(x, \cdot) - \pi P^t \|_{VT}$$

$$= \frac{1}{2} \sum_{z \in \mathcal{X}} \left| P^t(x, z) - \pi P^t(z) \right|$$

$$= \frac{1}{2} \sum_{z \in \mathcal{X}} \left| P^t(x, z) - \sum_{y \in \mathcal{X}} \pi(y) P^t(y, z) \right|$$

$$= \frac{1}{2} \sum_{z \in \mathcal{X}} \left| \sum_{y \in \mathcal{X}} \pi(y) (P^t(x, z) - P^t(y, z)) \right|$$

&emsp;Aplicando a **Desigualdade de Jensen** ($|E[h(Y)]| \le E[|h(Y)|]$ onde $Y \sim \pi$):

$$\le \frac{1}{2} \sum_{z \in \mathcal{X}} \left( \sum_{y \in \mathcal{X}} \pi(y) | P^t(x, z) - P^t(y, z) | \right)$$

$$= \sum_{y \in \mathcal{X}} \pi(y) \left( \frac{1}{2} \sum_{z \in \mathcal{X}} | P^t(x, z) - P^t(y, z) | \right)$$

$$= \sum_{y \in \mathcal{X}} \pi(y) \| P^t(x, \cdot) - P^t(y, \cdot) \|_{VT}$$

&emsp;Como a média ponderada é menor ou igual ao máximo:

$$\le \max_{y \in \mathcal{X}} \| P^t(x, \cdot) - P^t(y, \cdot) \|_{VT} \le \max_{x, y \in \mathcal{X}} \| P^t(x, \cdot) - P^t(y, \cdot) \|_{VT}$$

&emsp;**Conclusão**:

$$\max_{x \in \mathcal{X}} \| P^t(x, \cdot) - \pi \|_{VT} \le \max_{x, y \in \mathcal{X}} \| P^t(x, \cdot) - P^t(y, \cdot) \|_{VT}$$

---

## Acoplamento

$Def.:$ Um acoplamento de uma cadeia de Markov com matriz $P$ é um processo bivariado $(X_t, Y_t)_{t \ge 0}$ com a propriedade que ambos os processos $(X_t)_{t \ge 0}$ e $(Y_t)_{t \ge 0}$ são cadeias de Markov com matriz $P$.

Qualquer acoplamento $(X_t, Y_t)_{t \ge 0}$ pode ser modificado de forma que as cadeias fiquem juntas para sempre.

Uma vez que elas se encontram: $X_s = Y_s \implies X_t = Y_t, \forall t \ge s$.

Mais precisamente, definindo $\mathcal{T}_c = \min \{ s \ge 0 : X_s = Y_s \}$.

O acoplamento modificado $(\tilde{X}_t, \tilde{Y}_t)$ é definido por:

$$(\tilde{X}_t, \tilde{Y}_t) = \begin{cases} (X_t, Y_t) & \text{se } t < \mathcal{T}_c \\ (X_t, X_t) & \text{se } t \ge \mathcal{T}_c \end{cases}$$

---

### Teorema do Acoplamento

Se $X_0 = x$ e $Y_0 = y$, então para todo $t \ge 0$:

$$\| P^t(x, \cdot) - P^t(y, \cdot) \|_{VT} \le \mathbb{P}_{x,y}(\mathcal{T}_c > t) \le \frac{1}{t} \cdot \mathbb{E}_{x,y}[\mathcal{T}_c]$$

Desta desigualdade (utilizando a Desigualdade de Markov), temos:

$\implies \max_{x,y \in \mathcal{X}} \| P^t(x, \cdot) - P^t(y, \cdot) \|_{VT} \le \frac{1}{t} \max_{x,y \in \mathcal{X}} \mathbb{E}_{x,y}[\mathcal{T}_c]$.

$\implies$ Definindo $t_* = 4 \max_{x,y \in \mathcal{X}} \mathbb{E}_{x,y}[\mathcal{T}_c]$, temos que a distância é $\le 1/4$.

Portanto: **$t_{mix} \le 4 \max_{x,y \in \mathcal{X}} \mathbb{E}_{x,y}[\mathcal{T}_c]$**.

---

## Acoplamento para o P.A.P. no Anel

**Inicialização**: $X_0 = x$ e $Y_0 = y$.

**Dinâmica**:

1. A cada passo, joga-se uma moeda honesta para decidir qual dos passeios vai dar um passo.

2. Em seguida, o passeio escolhido move-se no sentido horário com probabilidade $1/2$ ou no sentido anti-horário com probabilidade $1/2$.

3. A partir do momento em que as cadeias se encontram, elas permanecem juntas.

Análise da Distância ($D_t$):

* Para cada $t$, defina $D_t$ como a distância no sentido horário entre $X_t$ e $Y_t$.
* Observe que $D_t \in \{0, 1, \dots, N\}$, com $D_0 = K$ (distância inicial entre $x$ e $y$).
* O tempo de acoplamento ocorre quando a distância atinge os limites: $\mathcal{T}_c = \min \{ t \ge 0 : D_t \in \{0, N\} \}$.

Pelo resultado da **Ruína do Jogador**:

$$\mathbb{E}_{x,y}[\mathcal{T}_c] = K \cdot (N - K) \le \frac{N}{2} \cdot \frac{N}{2} = \frac{N^2}{4}$$

**Conclusão**:

$$\max_{x,y} \mathbb{E}_{x,y}[\mathcal{T}_c] \le \frac{N^2}{4} \implies t_{mix} \le 4 \cdot \left( \frac{N^2}{4} \right) = N^2.$$