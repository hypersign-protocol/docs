# Circuits

### Arithmetic circuits <a href="#arithmetic-circuits" id="arithmetic-circuits"></a>

Circuit is like a program , which can be written in a programming language like Circom. However, internally a circuit is a **constraint system**; that is, a list of constraints which have a algebric forms;

{% hint style="info" %}
**Constraints:**

In order to use zk-SNARK protocols, we need to describe the relation between signals as a system of **equations** that relate variables with gates. The equations that describe the circuit is called **constraints.**&#x20;



Constraints **must be quadratic, linear or constant equations.** In general, circuits will have several constraints (typically, one per multiplicative gate). The set of constraints describing the circuit is called **rank-1 constraint system** (R1CS).&#x20;
{% endhint %}

* Since circuits are bit difficult for developers, we have programming languages (called DSL) for writing circuit logic. **Domain specific language (DSL)** : Circom, ZoKrates, Leo, Zinc, Cairo etc
* Once you written your program, it goes for compilation which converts the DSL into **SNARK friendly format** ([R1CS](https://tlu.tarilabs.com/cryptography/rank-1), AIR, plonk-CG etc)
* Once we convert into SNARK friendly format (constraint system), we generate public parameters (Sp, Sv) which is feeded into SNARK prover function to generate zk-proof.&#x20;

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Circom

`circom` allows programmers to define the [constraints](https://docs.circom.io/circom-language/constraint-generation) that define the arithmetic circuit. All constraints must be of the form `A*B + C = 0`, where `A`, `B` and `C` are linear combinations of signals. The arithmetic circuits built using `circom` operate on signals (inputs and outputs).

Zero-knowledge permits proving **circuit satisfiability**. What this means is, that you can prove that you know a set of signals that satisfy the circuit, or in other words, that you know a solution to the R1CS. This set of signals is called the **witness.**

