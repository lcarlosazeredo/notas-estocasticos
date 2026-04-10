# Aula 14

**Data:** 10/04/2026

**Defina:** $N(x) = \sum_{t=0}^{\infty} \mathbb{1}_{\{X_t = x\}}$, para cada $x \in \mathcal{X}$.
(Número de visitas a $x$).

**Lembre que:** $\mathcal{T}_x^+ = \min\{t \ge 1 : X_t = x\}$.
(Tempo de primeiro retorno).

---

### Proposição
$Prop.: \mathbb{P}_x(N(x) = \infty) = 1 \iff \mathbb{P}_x(\mathcal{T}_x^+ < \infty) = 1$.

**Definição:** O estado $x$ é **recorrente** se $\mathbb{P}_x(N(x) = \infty) = 1$.
Em particular, esta definição é equivalente à definição da aula passada.

---

### Prova da Proposição

**($\Rightarrow$)** É claro que $\{N(x) = \infty\} \subseteq \{\mathcal{T}_x^+ < \infty\}$.
$\Rightarrow 1 = \mathbb{P}_x(N(x) = \infty) \le \mathbb{P}_x(\mathcal{T}_x^+ < \infty) \le 1$.

**($\Leftarrow$)** Suponha $\mathbb{P}_x(\mathcal{T}_x^+ < \infty) = 1$.

Defina $\mathcal{T}_x^{+,k} = \min\{t \ge \mathcal{T}_x^{+,k-1} + 1 : X_t = x\}$ para $k \ge 1$, com $\mathcal{T}_x^{+,0} := 0$.

#### Afirmação (AF):
 $\mathbb{P}_x(\mathcal{T}_x^{+,k} < \infty) = 1, \quad \forall k \ge 1$.

Assumindo que a afirmação é verdade, temos que:
$\mathbb{P}_x\left(\bigcap_{k=1}^{\infty} \{\mathcal{T}_x^{+,k} < \infty\}\right) = 1$.
Como $\bigcap_{k=1}^{\infty} \{\mathcal{T}_x^{+,k} < \infty\} \subseteq \{N(x) = \infty\} \implies \mathbb{P}_x(N(x) = \infty) = 1$.

> **Verificar:** Se $A_k$ é evento e $P(A_k) = 1$, então $P(\bigcap_{k=1}^{\infty} A_k) = 1$.
> Isso decorre da continuidade da probabilidade.

#### Prova da AF:

Suponha que $\mathbb{P}_x(\mathcal{T}_x^{+,k} < \infty) = 1$.
Queremos mostrar que:
$\mathbb{P}_x(\mathcal{T}_x^{+,k+1} < \infty) = 1$.

Note que:

$$\mathbb{P}_x(\mathcal{T}_x^{+,k+1} < \infty) = \mathbb{P}_x \left( \mathcal{T}_x^{+,k+1} < \infty, \mathcal{T}_x^{+,k} < \infty \right) $$

$$= \mathbb{P}_x \left( \bigcup_{s=k}^{\infty} \{ \mathcal{T}_x^{+,k+1} < \infty, \mathcal{T}_x^{+,k} = s \} \right) $$

$$= \sum_{s=k}^{\infty} \mathbb{P}_x (\mathcal{T}_x^{+,k+1} < \infty, \mathcal{T}_x^{+,k} = s)$$

Fixe $s \ge k$:

$$\mathbb{P}_x (\mathcal{T}_x^{+,k+1} < \infty, \mathcal{T}_x^{+,k} = s) = \mathbb{P}_x \left( \bigcup_{t=s+1}^{\infty} \{ \mathcal{T}_x^{+,k+1} = t \}, \mathcal{T}_x^{+,k} = s \right)$$

$$= \sum_{t=s+1}^{\infty} \mathbb{P}_x (\mathcal{T}_x^{+,k+1} = t, \mathcal{T}_x^{+,k} = s)$$

---

Fixe $t \ge s + 1$:

$$\mathbb{P}_x (\mathcal{T}_x^{+,k+1} = t, \mathcal{T}_x^{+,k} = s) = \mathbb{P}_x (\mathcal{T}_x^{+,k} = s) \cdot \mathbb{P}_x (\mathcal{T}_x^{+,k+1} = t \mid \mathcal{T}_x^{+,k} = s, X_{\mathcal{T}_x^{+,k}} = x)$$

Pela **Propriedade Forte de Markov**:

$$= \mathbb{P}_x (X_1 \neq x, X_2 \neq x, \dots, X_{(t-s)-1} \neq x, X_{t-s} = x)$$



$$\therefore \mathbb{P}_x (\mathcal{T}_x^{+,k+1} = t, \mathcal{T}_x^{+,k} = s) = \mathbb{P}_x (\mathcal{T}_x^{+,k} = t) \cdot \mathbb{P}_x (\mathcal{T}_x^{+,k} = s)$$

$\Rightarrow$

$$\mathbb{P}_x (\mathcal{T}_x^{+,k+1} < \infty, \mathcal{T}_x^{+,k} = s) = \mathbb{P}_x (\mathcal{T}_x^{+,k} = s) \sum_{h=1}^{\infty} \mathbb{P}_x (\mathcal{T}_x^{+,1} = h)$$

$$= \mathbb{P}_x (\mathcal{T}_x^{+,k} = s) \mathbb{P}_x \left( \bigcup_{h=1}^{\infty} \{ \mathcal{T}_x^{+,1} = h \} \right)$$

$$= \mathbb{P}_x (\mathcal{T}_x^{+,k} = s) \mathbb{P}_x \left( \mathcal{T}_x^{+,1} < \infty \right)$$

---

$\Rightarrow$

$$\mathbb{P}_x (\mathcal{T}_x^{+,k+1} < \infty) = \mathbb{P}_x (\mathcal{T}_x^{+,1} < \infty) \sum_{s=k}^{\infty} \mathbb{P}_x (\mathcal{T}_x^{+,k} = s)$$

$$= \mathbb{P}_x (\mathcal{T}_x^{+,1} < \infty) \mathbb{P}_x \left( \bigcup_{s=k}^{\infty} \{ \mathcal{T}_x^{+,k} = s \} \right)$$

$$= \mathbb{P}_x (\mathcal{T}_x^{+,1} < \infty) \mathbb{P}_x (\mathcal{T}_x^{+,k} < \infty)$$

Logo:

$$\mathbb{P}_x (\mathcal{T}_x^{+,k+1} < \infty \mid \mathcal{T}_x^{+,k} < \infty) = \mathbb{P}_x (\mathcal{T}_x^{+,1} < \infty)$$

> **Verificar:** $X$ v.a. $\ge 0$ discreta em $\mathbb{N}: \{X < \infty\} = \bigcup_{x=0}^{\infty} \{X = x\}$

---

### Proposição
$Prop.:$ Todos os estados de uma C.M. **irredutível (e FINITA)** são recorrentes. Mais precisamente:

$$\mathbb{E}_y [\mathcal{T}_x^+] < \infty, \quad \forall x, y \in \mathcal{X}$$

#### Afirmação 1:
**Af. 1:** $\exists r \ge 1$ e $\epsilon > 0$ t.q.

$$\mathbb{P}_y \left( \bigcup_{s=1}^{r} \{ X_{t+s} = x \} \mid X_t = z \right) > \epsilon $$

para todo $t \ge 0$ e $x, y, z \in \mathcal{X}$.

#### Prova da Afirmação 1:
**Prova Af. 1:** Como a cadeia é irredutível, para quaisquer estados $z$ e $w$ existe $t = t(z,w) > 0$ t.q. $P_{(z,w)}^{t(z,w)} > 0$.

Defina $r = \min\{t(z,w) : z, w \in \mathcal{X}\}$
e
$\epsilon = \frac{1}{2} \cdot \min\{P_{(z,w)}^{t(z,w)} : z, w \in \mathcal{X}\}$.

Pela prop. Markov:

$$\mathbb{P}_z \left( \bigcup_{s=1}^{r} \{ X_{t+s} = x \} \mid X_t = z \right) = \mathbb{P}_z \left( \bigcup_{s=1}^{r} \{ X_s = x \} \right)$$

$$\ge \mathbb{P}_z ( \{ X_{t(z,x)} = x \} )$$

$$= P_{(z,x)}^{t(z,x)} > \epsilon $$



