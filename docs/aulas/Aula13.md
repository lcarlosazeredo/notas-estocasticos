# Aula 13

**Data:** 08/04/2026

## Revisão

* **$\mathcal{T}$ = tempo de parada**: $\mathcal{T} \in \mathbb{N} \cup \{\infty\}$.
* $\forall t \ge 0$: o evento $\{\mathcal{T} = t\}$ só depende de $X_0, \dots, X_t$.

### Exemplo:
* $\mathcal{T}_A = \min\{t \ge 0 : X_t \in A\}$, $A \subseteq \mathcal{X}$ (tempo de primeira visita).
* $\mathcal{T}_A^+ = \min\{t \ge 1 : X_t \in A\}$ (tempo de primeiro retorno).

Quando $A = \{x\}$:

* $\mathcal{T}_A =: \mathcal{T}_x$.
* $\mathcal{T}_A^+ =: \mathcal{T}_x^+$.

---

## Definição

$Def.:$ Dizemos que um estado $x$ é **recorrente** se:

$$\mathbb{P}_x(\mathcal{T}_x^+ < \infty) = 1$$

> **Verificar:**
> $X>0: E[X] < \infty \Rightarrow \mathbb{P}(X < \infty) = 1$.



---

## Proposição

$Prop.:$ Se $\mathcal{X}$ é finito e a cadeia é irredutível, então $\mathbb{E}_x[\mathcal{T}_y^+] < \infty$ para todos os estados $x$ e $y$.

Em particular:

&emsp;&emsp;$\mathbb{P}_x(\mathcal{T}_y^+ < \infty) = 1, \forall x,y \in \mathcal{X}$

&emsp;&emsp;E todos os estados são recorrentes.