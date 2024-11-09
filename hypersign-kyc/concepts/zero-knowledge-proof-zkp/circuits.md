# Circuits

* Since circuits are bit difficult for developers, we have programming languages (called DSL) for writing circuit logic. **Domain specific language (DSL)** : Circom, ZoKrates, Leo, Zinc, Cairo etc
* Once you written your program, it goes for compilation which converts the DSL into **SNARK friendly format** (R1CS, AIR, plonk-CG etc)
* Once we convert into SNARK friendly format, we generate public parameters (Sp, Sv) which is feeded into SNARK prover function along with witness to generate zk-proof.&#x20;

