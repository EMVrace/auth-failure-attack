# Authentication Failure Attack

This repository contains the complementary material for our Usenix'23 paper *Inducing Authentication Failures to Bypass Credit Card PINs*. The material include:

- [`Contactless.spthy`](./Contactless.spthy): The modified version of our previous EMV contactless protocol [model](https://github.com/EMVrace/EMVerify)
- [`attack-trace.png`](./attack-trace.png): The attack trace corresponding to our authentication failure attack found by Tamarin using our modified model

To replicate the attack finding experiment, run the following steps:

1. Download Basin et al model from https://github.com/EMVrace/EMVerify
2. Replace the file `Contactless.spthy` with our modified version provided here
3. Run `make kernel=Mastercard auth=CDA CVM=NoPIN value=High lemma=executable` and inspect the analysis results will be in `models-n-proofs/contactless/Mastercard_CDA_NoPIN_High.proof`.<br >To reproduce the graphical attack trace above, run Tamarin in interactive mode on the theory file `models-n-proofs/contactless/Mastercard_CDA_NoPIN_High.spthy` (please read the Tamarin [manual](https://tamarin-prover.github.io/manual/book/001_introduction.html) to run the tool in this mode).
