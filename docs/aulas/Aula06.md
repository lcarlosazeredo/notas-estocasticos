# Aula 6 - 20/03/2026

## Revisão

$(X_t)_{t \ge 0}$ C.M. com matriz de transição $P$

$(X_t)_{t \ge 0}$ é irredutível se:
$\forall x, y \in \mathcal{X}, \exists t = t(x, y) \ge 0$ t.q.
$P_x(X_t = y) = P^t(x, y) > 0$

Definimos,
$\mathcal{J}(x) = \{ t \ge 1 : P^t(x, x) > 0 \}$
é o conjunto de instantes de tempo em que a cadeia retorna ao ponto inicial $x$.

O período de $x$ é definido como $\text{mdc } \mathcal{J}(x)$

**Prop:** Todos os estados de uma C.M. irredutível têm o mesmo período.

**Prova.** Precisamos mostrar que $\text{mdc } \mathcal{J}(x) = \text{mdc } \mathcal{J}(y)$, $\forall x, y \in \mathcal{X}$.
Fixe $y$ e $x$ estados da cadeia e denote $d_y = \text{mdc } \mathcal{J}(y)$.
Vamos mostrar que $d_y$ divide todos os elementos de $\mathcal{J}(x)$, o que garante que $\text{mdc } \mathcal{J}(x) \ge d_y$.
Tome $t \in \mathcal{J}(x) \Rightarrow P^t(x, x) > 0$.
Pela irredutibilidade $\exists L, R$ t.q. $P^L(y, x) > 0$ e $P^R(x, y) > 0$.
Logo, em $L + t + R$ passos a cadeia saindo de $y$ retorna a $y$ passando por $x$ com prob. positiva.

---

## Distribuições Estacionárias

Seja $\nu$ uma medida de prob. inicial.
$\mu_t(y) = \mathbb{P}_\nu(X_t = y) = \sum_{x \in \mathcal{X}} \nu(x) P^t(x, y)$

Se existe uma dist. estacionária $\pi$:
$\pi(y) = \lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} \mu_t(y)$
$\pi(y) = \lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} \sum_{x \in \mathcal{X}} \nu(x) P^t(x, y)$
$\pi(y) = \lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} \mathbb{P}_\nu(X_t = y)$
$\pi(y) = \lim_{T \to \infty} \mathbb{E}_\nu \left[ \frac{1}{T} \sum_{t=0}^{T-1} \mathbb{1}_{\{X_t = y\}} \right]$

### Estimador

Denotando $\hat{N}_{T-1}(y) = \sum_{t=0}^{T-1} \mathbb{1}_{\{X_t = y\}}$ (número de visitas a $y$ até $T-1$):

$\pi(y) = \lim_{T \to \infty} \mathbb{E}_\nu \left[ \frac{\hat{N}_{T-1}(y)}{T} \right]$

O estimador $\frac{\hat{N}_{T-1}(y)}{T}$ é **assintoticamente não-viesado** para $\pi(y)$.

O Teorema Ergódico (a ser visto mais adiante)
$\frac{\hat{N}_{T-1}(y)}{T}$ é um estimador **consistente** para $\pi(y)$, se $P$ é irredutível.

A convergência ocorre quase certamente (o estimador é consistente):
$\mathbb{P}_\nu \left( \lim_{T \to \infty} \frac{\hat{N}_{T-1}(y)}{T} = \pi(y) \right) = 1$