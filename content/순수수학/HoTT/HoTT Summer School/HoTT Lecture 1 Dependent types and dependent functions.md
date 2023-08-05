## Natural Deduction (자연 연역)
proof tree 그리기 간단하게 알아보자.
see [Logic and Proof](https://leanprover.github.io/logic_and_proof/).

We use proof trees built out of rules.

Ex) Want to show $Q$ from $P\cap (P \rightarrow Q)$
(Think that $P$ and $Q$ are arbitrary propositions)

-> How to prove this in natural deduction?


During the example, we will introduce some allowed rules in natural deduction
(1) we can deduce one particular holds.
$$
\dfrac{P \land (P \rightarrow Q)}{P}
$$
if it stands for the left, we say it $\wedge \verb|-elim-l|$.

$$
\dfrac{P \land (P \rightarrow Q)}{P \rightarrow Q}
$$
Similarly, if it stands for the right, we say it $\wedge \verb|-elim-r|$. 


(2) implication[^1] elimination (we write it like $\verb|-elim|$)
$$
\dfrac{ {\dfrac{P \land (P \rightarrow Q)}{P} }{\dfrac{P \land (P \rightarrow Q)}{P \rightarrow Q} } }{Q}  
$$
[^1]: implication(조건명제, 함의)란 $p\rightarrow q$ 와 같은 명제에서 해당 명제가 참일때를 의미한다. 일반적으로 $p\Rightarrow q$ 와 같이 표기한다. 


As we checked at the example, let's expand to the general case.



Rules for $\wedge$: 

(1) $\wedge \verb|-intro|$
If we know the two propositions $P$ and $Q$, we can deduce(추론) $P\wedge Q$. It could be expressed as
$$
\frac{P\,\,\,\,\,\,\, Q}{P \wedge Q}
$$
Q) What is the difference between implication arrow and horizontal deduction bar?
We could interpret $\rightarrow$ as 'internal', $-$ as 'external'. [^2]

[^2]: 즉, 추론 바($-$)는 실제 명제 증명 구조(structure)의 일부이기 때문에 외부적인 느낌이 강하고, $\rightarrow$는 조금 더 내부적인 느낌이 강하다. 이에 대한 더 자세한 차이점은 앞으로의 수업에서 다루게 될 것이다.

(2) $\wedge \verb|-elim-l|$ & $\wedge \verb|-elim-r|$
$$
\begin{align}
\frac{P \wedge Q}{P} \,\,\,\,\,(\wedge \verb|-elim-l|) \\\\
\frac{P \wedge Q}{Q} \,\,\,\,\,(\wedge \verb|-elim-r|)
\end{align}
$$

Also there is a rule for implication($\rightarrow$),

(1) $\rightarrow \verb|-intro|$

$$
\begin{gathered}
\bar{P}^{\prime} \\
\vdots \\
\frac{Q}{P \rightarrow Q}{ }^{\prime}
\end{gathered}
$$
#이해안됨 저게 뭐임? 저기에 bar는 왜 있는 것이며 프라임은 왜 드감?


(2)$\rightarrow \verb|-elim|$
$$
\frac{P\,\,\,\,\,\, P\rightarrow Q}{Q}
$$

Ex)
$(P\wedge Q) \rightarrow P$
$$
\dfrac{\dfrac{P \wedge Q}{P} \,\,(\wedge \verb|-elim-l|)}{(P \wedge Q) \rightarrow P}\,\,(\rightarrow \verb|- intro|)
$$

## Simply Typed $\mathbb{\Lambda}$ Calculus

In natural deduction, write "$P$" to mean "$P$ holds".
In ST$\Lambda$C, write "$p:P$" to mean "$p$ is a proof/witness of $P$" [^3]
[^3]: or, "$P$ holds by virtue of the proof $p$"

In ST$\Lambda$C, we are doing same as ND but now it's proof relevant.
We call $p$ a term of type $P$.

Ex)  show $Q$ from $P\cap (P \rightarrow Q)$
$$
\dfrac{{\dfrac{a:P \land (P \rightarrow Q)}{\mathrm{pr_1}a:P}}\,\,\,{\dfrac{a:P \land (P \rightarrow Q)}{\mathrm{pr_2}a:P \rightarrow Q}}}{(\mathrm{pr_2}a)(\mathrm{pr_1}a):Q}  
$$

Rules for $\wedge$: 

(1) $\wedge \verb|-form|$ (formation rule)
$$
\dfrac{P\,\,is\,\, \verb|type|\,\,\,\, Q \,\,is\,\,\verb|type|}{P \wedge Q \,\,is\,\, \verb|type|}
$$

(2) $\wedge \verb|-intro|$ (introduction rule)
$$
\dfrac{p:P\,\,\,\,q:Q}{(p,q): P\wedge Q}
$$
(3) $\wedge \verb|-elim|$ (elimination rule)
$$
\begin{align}
\frac{a:P \wedge Q}{\mathrm{pr_{1}}a:P} \,\,\,\,\,(\wedge \verb|-elim-l|) \\\\
\frac{a:P \wedge Q}{\mathrm{pr_{2}}a:Q} \,\,\,\,\,(\wedge \verb|-elim-r|)
\end{align}
$$
(4) $\wedge \verb|-comp-|\beta$ (computation rule)
$$
\begin{align}
\frac{p:P \,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\, q:Q}{\mathrm{pr_{1}}(p,q)\doteq p:P} \,\,\,\,\,(\wedge \verb|-comp-|\beta\verb|-l|) \\\\
\frac{p:P \,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\, q:Q}{\mathrm{pr_{2}}(p,q)\doteq q:Q} \,\,\,\,\,(\wedge \verb|-comp-|\beta\verb|-r|)
\end{align}
$$
(5) $\wedge \verb|-comp-|\eta$ (computation rule)
$$
\begin{align}
\frac{a:P\wedge Q}{(\mathrm{pr_{1}}a,\mathrm{pr_{2}}a)\doteq a:P\wedge Q} \,\,\,\,\,(\wedge \verb|-comp-|\eta)
\end{align}
$$
[^4]
[^4]: So what $\doteq$ means?

$\mathrm{Thm.(Lambek,\,1985)}$
$\begin{align}&\mathrm{There\,is\,an\,interpertation\,of\,the\,ST\Lambda C\,with\,\wedge\,and\,\rightarrow into\,Set,\,the\,category\,of\,sets.}\\&\mathrm{(Actually\,there\,is\,a\,equivalence\,with\,CCC(Cartesian\,Closed\,Categories).)}\end{align}$


Rules for $\rightarrow$:

(1) $\rightarrow \verb|-form|$
$$
\dfrac{P\,\,is\,\, \verb|type|\,\,\,\, Q \,\,is\,\,\verb|type|}{P \wedge Q \,\,is\,\, \verb|type|}
$$
(2) $\rightarrow \verb|-intro|$
$$
\dfrac{a\, \mathrm{proof\, of }\,Q\, \mathrm{from} \,P}{P \rightarrow Q} \rightarrow \dfrac{\Gamma, x:P \vdash q:Q}{\Gamma \vdash \lambda x. q:P\rightarrow Q}
$$
Now we need contexts, and we want every rule to hold in every context.

(3) $\rightarrow \verb|-elim|$
$$
\dfrac{\Gamma \vdash f:P\rightarrow Q \,\,\,\,\,\,\, \Gamma \vdash p:P}{\Gamma \vdash fp:Q}
$$
(4) $\rightarrow \verb|-comp-|\beta$
$$
\dfrac{\Gamma, x:P \vdash q: Q \,\,\,\,\,\,\, \Gamma \vdash p:P}{\Gamma \vdash (\lambda x.q)(p)\doteq q[p/x]}
$$
