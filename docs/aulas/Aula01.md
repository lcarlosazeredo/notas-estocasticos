# Aula 1:

**Data:** 09/03  
**Professor:**   
**Referência:** Sheldon Ross: Introduction to Probability Models  
&emsp;&emsp;&emsp;&emsp;&emsp;  Valle & Vares: Processos Estocásticos

## Ementa
* Cadeias de Markov a tempo discreto.
* Processo de Poisson e variações.
* Cadeias de Markov a tempo contínuo.
* Martingais.
* Movimento Browniano (se houver tempo).

**Avaliação:** 2 Provas.

---

## 1. Cadeia de Markov (Tempo Discreto)

### Exemplo 1 (A Ruína do Jogador)
* A cada jogada, um apostador ganha R$ 1,00 com prob. $p$ e perde R$ 1,00 com prob. $1-p$ ($p \in [0, 1]$).
* O jogo acaba quando o apostador atinge a fortuna $N$ ou quando ele fica sem dinheiro.
* **Espaço de Estados:** $\{0, 1, 2, \dots, N\}$ (possíveis valores que a v.a. pode assumir).
* **Estados Absorventes:** $0$ e $N$ (estados onde o processo para).

**Perguntas:**
1. Qual a probabilidade de o jogador atingir a fortuna?  
&emsp;&emsp;&emsp;&emsp;&emsp;2. Em média, qual é o número de apostas até o jogo acabar?

**Respostas para 1&2:**
1. Se a quantia inicial do jogador é $0 \le k \le N$, a prob. de atingir a fortuna é ${k}/{N}$.    
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;2. O número médio de apostas é $k(N-k)$.

### Exemplo 2 (Passeio Aleatório em $\mathbb{Z}$)
Um indivíduo salta para a direita com prob. $p$ e para a esquerda com prob. $1-p$.
  
* **Pergunta:** Para quais valores de $p$ o indivíduo visita a origem infinitas vezes com prob. 1?  
* **Resposta:** Somente para $p = 1/2$ (neste caso, o processo é recorrente).  

### Exemplo 3 (P.A.S. em $\mathbb{Z}^2$)
* O passeio visita a origem infinitas vezes com prob. 1? **Sim!**

### Exemplo 4 (P.A.S. em $\mathbb{Z}^3$)
* O passeio visita a origem infinitas vezes com prob. 1? **Não!**

---

## 2. Definição de Cadeia de Markov (Tempo Homogêneo)
  
$(X_{n})_{n \ge 0}$ uma seq. de V.A.'s tais que as seguintes propriedades valem:  
1. $X_n \in \mathcal{X}, \forall n \ge 0$.  
2. $\mathbb{P}(X_{n+1} = y \mid X_n = x, X_{n-1} = x_{n-1}, \dots, X_0 = x_0) = \mathbb{P}(X_{n+1} = y \mid X_n = x) = p_{xy}$.  

* **Espaço de Estados ($\mathcal{X}$):** Conjunto finito ou enumerável.
* $p_{xy}$ é a probabilidade de visitar o estado $y$ dado que a cadeia está no estado $x$.

### Exemplo (P.A. em $\mathbb{Z}$):
$\mathcal{X} = \mathbb{Z}$

$$
p_{xy} = 
\begin{cases} 
p, & \text{se } y = x+1 \\
1-p, & \text{se } y = x-1 \\
0, & \text{c.c.}
\end{cases}
$$

### Matriz de Transição ($P$)
Denotamos $P = (p_{xy})_{x,y \in \mathcal{X}}$. 

**Propriedades (Matriz Estocástica):**  
&emsp;1. $p_{xy} \ge 0, \forall x,y \in \mathcal{X}$  
&emsp;2. $\sum_{y \in \mathcal{X}} p_{xy} = 1, \forall x \in \mathcal{X}$  

!!! info "Simulação Interativa Disponível"
    [Acessar Simulador :material-open-in-new:](../simulacoes/markov_simulations[1].html){: .md-button target="_blank" }
    
