**Submission-Ready Paper (Core Version)**
=========================================

**Title**
---------

When Does Feedback Require Representation?

A Testable Criterion for Cybernetic Control

**Abstract**
------------

We formalize a distinction between direct physical feedback and
goal-directed cybernetic control. While both are commonly described
under a single notion of feedback, they differ in their structural
requirements. We prove that a system exhibits cybernetic feedback if and
only if its internal state carries task-relevant information about
external variables beyond current observation and is causally used to
achieve strictly better control than any reactive policy. This yields a
measurable criterion based on conditional mutual information I(m\_t;
z\_t \\mid y\_t) and performance separation. We validate the framework
on partially observable control tasks, showing that recurrent agents
exhibit positive conditional mutual information and outperform reactive
baselines under delay and occlusion. This reframes representation as a
testable property of control systems rather than a purely philosophical
construct.

**1. Introduction**
-------------------

The concept of feedback is used across physics, biology, and engineering
to describe systems that regulate their behavior in response to their
state. However, two distinct phenomena are often conflated:

-   Physical feedback: direct coupling between system state and response
    > (e.g., thermodynamic equilibration)

-   Cybernetic feedback: goal-directed control based on internal state
    > (e.g., adaptive systems, organisms, controllers)

This paper addresses the question:

> When does feedback require an internal representation of the world?

We provide:

-   A formal definition of representation grounded in control theory

-   A necessary and sufficient condition for cybernetic feedback

-   Empirical methods to test this condition

**2. Model**
------------

We consider a discrete-time controlled system:

-   x\_t \\in \\mathcal{X}: world state

-   y\_t \\in \\mathcal{Y}: observation

-   m\_t \\in \\mathcal{M}: internal state

-   a\_t \\in \\mathcal{A}: action

Dynamics:

x\_{t+1} \\sim P(\\cdot \\mid x\_t, a\_t)

Observations:

y\_t \\sim O(\\cdot \\mid x\_t)

Internal update:

m\_{t+1} = U(m\_t, y\_{t+1}, a\_t)

Policy:

a\_t \\sim \\pi(\\cdot \\mid m\_t)

**3. Reactive vs Internal-State Policies**
------------------------------------------

Define two classes:

-   Reactive (PF):\
    > \
    > \\Pi\_{\\text{pf}} = \\{\\pi(a\_t \\mid y\_t)\\}

-   Internal-state (CF):\
    > \
    > \\Pi\_{\\text{cf}} = \\{\\pi(a\_t \\mid m\_t)\\}

**4. Representation as Conditional Information**
------------------------------------------------

Let z\_t = f(x\_t) be task-relevant external variables.

We define:

> Representation exists when

I(m\_t; z\_t \\mid y\_t) \> 0

Interpretation:

-   Internal state contains information about the world

-   Beyond what is available in current observation

**5. Main Result**
------------------

**Proposition 1 (Feedback Theorem)**
------------------------------------

A system exhibits cybernetic feedback if and only if there exists a
policy \\pi \\in \\Pi\_{\\text{cf}} such that:

1.  Representation condition\
    > \
    > I(m\_t; z\_t \\mid y\_t) \> 0

2.  Causal use\
    > \
    > \\pi(a \\mid m) \\neq \\pi(a \\mid m\') \\text{ for some } m \\neq
    > m\'

3.  Performance separation\
    > \
    > J(\\pi) \< \\inf\_{\\tilde{\\pi} \\in \\Pi\_{\\text{pf}}}
    > J(\\tilde{\\pi})

**6. Interpretation**
---------------------

-   \(1\) → internal model exists

-   \(2\) → model is used

-   \(3\) → model is necessary

Together, these define cybernetic feedback.

**7. Experimental Validation**
------------------------------

### **7.1 Setup**

We use partially observable environments where:

-   y\_t does not uniquely determine x\_t

-   memory improves performance

### **7.2 Agents**

-   Feedforward (FF): a\_t \\sim \\pi(y\_t)

-   Recurrent (RNN): a\_t \\sim \\pi(m\_t)

### **7.3 Metrics**

#### **(A) Performance**

J(\\pi)

#### **(B) Conditional Mutual Information (estimated)**

Using predictive gain:

\\hat{I} = \\mathbb{E}\[\\log p(z\|m,y) - \\log p(z\|y)\]

### **7.4 Experiments**

### **Experiment 1 --- Representation Emergence**

-   Train FF and RNN agents

-   Measure \\hat{I}

Expected:

-   FF ≈ 0

-   RNN \> 0

### **Experiment 2 --- Performance Separation**

Compare:

-   J(\\pi\_{\\text{FF}})

-   J(\\pi\_{\\text{RNN}})

Expected:

-   RNN strictly better

### **Experiment 3 --- Memory Ablation**

-   Shuffle or reset m\_t

Measure:

\\Delta J = J\_{\\text{ablated}} - J\_{\\text{original}}

Expected:

-   Large degradation

### **Experiment 4 --- Occlusion Test**

-   Temporarily hide observations

Expected:

-   FF fails

-   RNN maintains performance

**8. Results (Expected Pattern)**
---------------------------------

  **Metric**             **FF**   **RNN**
  ---------------------- -------- ---------
  I(m;z\|y)              \~0      \>0
  Performance            lower    higher
  Ablation sensitivity   none     high

**9. Discussion**
-----------------

This provides a testable criterion for representation:

> Representation is not assumed---it is measured via control-relevant
> information.

Implications:

-   clarifies feedback in biology and AI

-   separates physical and cybernetic systems

-   enables empirical study of representation

**10. Limitations**
-------------------

-   MI estimation is approximate

-   depends on task variable z\_t

-   does not address consciousness

**11. Conclusion**
------------------

Cybernetic feedback arises precisely when internal state:

-   carries task-relevant information

-   is causally used

-   improves control beyond reactive limits

This reframes representation as a measurable property of systems.
