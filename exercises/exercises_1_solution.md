## 1. Correctness of the Determinization Construction

Complete the proof of correctness of the determinization construction.

Let `N` be a NFA and `D` be a DFA obtained from `N` using the powerset construction.
Show that any word accepted by `D` is also accepted by `N`: `w ∈ L(D) ⇒ w ∈ L(N)`.

### Solution :

If $D = (Q_D, Σ, δ_D, \lbrace q_0 \rbrace, F_D)$ is the DFA constructed from NFA $N = (Q_N, Σ, δ_N, q_0, F_N)$ by the `subset construction / powerset construction` _( Method for converting a nondeterministic finite automaton (NFA) into a deterministic finite automaton (DFA))_. 

Then $w ∈ L(D) ⇒ w ∈ L(N)$

#### Proof :
- By Induction on $|w|$ is that, $\hat{\delta}_D(\lbrace q_0 \rbrace,w) = \hat{\delta}_N(q_0,w)$

  Notice that each of $\hat{\delta}$ functions returns a set of states from $Q_N$, but the $\hat{\delta}_D$ inteprets as one set of the states of $Q_D$ (which is the powerset of $Q_N$). While, $\hat{\delta}_N$ inteprets this as a subset of $Q_N$.

- Let $|w| = 0$; that is, $w= \epsilon$. 

  By the basis definition of $\hat{\delta}$ for DFA and NFA, both $\hat{\delta}_D(\lbrace q_0 \rbrace,w)$ and $\hat{\delta}_N(q_0,w)$ are $\lbrace q_0 \rbrace$

- Let $w$ be of length $n+1$, and assume that the statement for length $n$. Break $w$ up as $w=xa$, where $a$ is the final symbol of $w$. By using the inductive hypothesis, $\hat{\delta}_D(\lbrace q_0 \rbrace,x) = \hat{\delta}_N(q_0,x)$. Let both of these sets of N's states be $\lbrace p_1,p_2,p_3,...,p_k \rbrace$.

  - The inductive part of the definition of $\hat{\delta}_D$ for NFA's tell us: $\hat{\delta}_N(q_0, w) = \bigcup _{i=1}^k \delta_N(p_i, a)$  $...(1.1)$

  - The subset construction, on the other hand tells us that: $\hat{\delta}_D(\lbrace p_1,p_2,p_3,...,p_k \rbrace, a) = \bigcup _{i=1}^k \delta_N(p_i, a)$ $...(1.2)$

  - Now, let us use $(1.2)$ and the fact that $\hat{\delta}_D(\lbrace q_0 \rbrace,x) = \lbrace p_1,p_2,p_3,...,p_k \rbrace$ in the inductive part of the definition of $\hat{\delta}_D$ for for DFA's:

    $\hat{\delta}_D(\lbrace q_0 \rbrace,w) = \delta_D ( \hat{\delta}_D(\lbrace q_0 \rbrace,x),a) = \delta_D( \lbrace p_1,p_2,p_3,...,p_k \rbrace ,a) = \bigcup _{i=1}^k \delta_N(p_i, a)$ $...(1.3)$
  
- Thus, Equations $(1.1)$ and $(1.3)$ demonstrate that $\hat{\delta}_D(\lbrace q_0 \rbrace,w) = \hat{\delta}_N(q_0,w)$. 

- When we observe that D and N both accept $w$ if and only if $\hat{\delta}_D(\lbrace q_0 \rbrace,w)$ or $\hat{\delta}_N(q_0,w)$, respectively, contains a state in $F_N$, we have complete proof that $L(D) = L(N)$



## 2. Encoding Programs as Automaton

Recall the lock automaton:

```graphviz
digraph finite_state_machine {
    rankdir=LR;
    node [shape = doublecircle];
    init [shape = none, label = ""];
    init -> U;
    U -> L [ label = "lock" ];
    L -> U [ label = "unlock" ];
}
```

And the increment program:
```c
int balance;

void increase(int x) {
    lock();
    balance += x;
    unlock();
}
```
and the corresponding automaton:
```graphviz
digraph finite_state_machine {
    rankdir=LR;
    node [shape = doublecircle];
    init [shape = none, label = ""];
    init -> 0;
    0 -> 1 [ label = "lock" ];
    1 -> 2 [ label = "balance += x" ];
    2 -> 3 [ label = "unlock" ];
}
```

__Tasks 1.__
Generalize this example to use a `semaphore` instead of a lock.
A semaphore generalize a lock with counting.
The equivalent of `lock` is `acquire` and `release` instead of `unlock`.
However a semaphore allows up to `n` processes to `acquire` permits before a process releases one permit.
`n` is a parameter given during the creation of the semaphore.

Instantiate your example with 3 `increase` program and a semaphore with `n=2`.

You are allowed to change the automata (states, alphabet, transition, etc.).
If this is possible, suggest an alternate model where this is possible.

### Solution


__Task 2.__
Generalize this example to make the lock _reentrant_.
A reentrant lock allows one thread to `lock` the same lock multiple times.
The lock must be `unlock`ed the same number of times it was `lock`ed before a new process can acquire it.

You are allowed to change the automata (states, alphabet, transition, etc.).
If this is possible, suggest an alternate model where this is possible.

### Solution



## 3. Longest (Worst Case) Shortest Counterexample to a Safety Property for Automata

Consider the setting where we have a program and a safety property encoded as automata.
For instance, this is the setting of the previous example.
Let us further assume that the automaton are DFAs.

* Assume the automaton for the program has `m` states, the property has `n` states, and the program does not respect the property.
  This means that the product of the program and the negated property is non-empty.
  In the worst case, how long is the shortest word in the product of the program and the negated property?
* Can you construct an example that reaches your bound?
* Prove your bound
* What happens when there are many copies of the program (e.g. concurrency)? _hint._ this is one of the reason testing concurrent programs is hard.

### Solution



## 4. The Need for Multiple Final States for DFAs

Assume a DFA can have at most one final state. 
Show that there is a regular language `L` over a unary alphabet ($\Sigma = \\{ a \\}$) which is not recognizable with this model,
i.e. there is no DFA with a single final state whose language `L`.
Prove your claim.

### Solution
