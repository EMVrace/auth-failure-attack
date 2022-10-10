# Authentication Failure Attack

This repository contains the complementary material for our Usenix'23 paper *Inducing Authentication Failures to Bypass Credit Card PINs*. The material include:

- [`Contactless.spthy`](./Contactless.spthy): The modified version of our previous EMV contactless protocol [model](https://github.com/EMVrace/EMVerify).
- [`attack-trace.png`](./attack-trace.png): The attack trace corresponding to our authentication failure attack found by Tamarin using our modified model.

## Replicate the attack finding experiment

First, you must have the following software installed and properly referenced:
- Tamarin (see installation instructions [here](https://tamarin-prover.github.io/manual/book/002_installation.html))
- Python 2 (the scripts [`Mastercard.oracle`](./Mastercard.oracle) and [`tools/decomment`](./tools/decomment) use this Python version.<br />
Should you want to use Python 3, you'll need to adapt these two scripts by properly referencing the executable programs `#!/usr/bin/python3` and adding parentheses to Python's `print` calls in the scripts' source)

To find our attack with the tool, now follow the steps below:
1. Download our original model from https://github.com/EMVrace/EMVerify.
1. Replace the file `Contactless.spthy` with our modified version provided here.
1. Delete the folder `models-n-proofs`.
1. Run
```shell
make -s kernel=Mastercard auth=CDA CVM=NoPIN value=High lemma=executable
```
and the proof that such insecure execution (PIN-less & high-value) exists will be at `models-n-proofs/contactless/Mastercard_CDA_NoPIN_High.proof`.
1. [Optional] To reproduce the graphical attack trace above, run Tamarin in interactive mode:
```shell
tamarin-prover interactive models-n-proofs/contactless/Mastercard_CDA_NoPIN_High.spthy --heuristic=O --oraclename=Mastercard.oracle
```
and follow the instructions. Please refer to the Tamarin [manual](https://tamarin-prover.github.io/manual/book/001_introduction.html) for more on the tool's interactive mode.

