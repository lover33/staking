<p align="center">
  <img
    src="https://cdn-images-1.medium.com/letterbox/164/72/50/50/1*bGf9HZHNP3tOk4dSWcxUHA.png?source=logoAvatar-lo_dnt_VASJhQluBeQP---b71bf4ba23ad"
    width="100px;">

</p>
<h3 align="center">Nash Exchange Token (NEX) Staking Smart Contract</h3>
<hr/>



# Overview

This smart contract allows holders of the  Nash Exchange token (NEX) to `stake` them in this contract in order to receive a portion of fees generated by the Nash exchange.

The staking contract implements the following:
- Any address that wishes to stake their Nash Exchange tokens must go through the KYC process within the Nash platform. Once they have done so, they will be eligible to stake any amount of tokens they hold.
- In order to `stake` tokens, a user must call the `approve` method on the Nash token contract (`0x3a4acd3647086e7c44398aac0349802e6a171129`) to permit the staking contract to transfer X amount of tokens from their wallet address to the staking contract.
- The duration of the stake is specified in months, between 1 and 24.
- The amount to be staked must be divisible by `1 * 10 ^ 8`, or 100000000.  This simplifies the distribution of exchange fees.
- Once a set of tokens has been staked, there is **no** method of retrieving them from the contract until the stake period specified by the user has expired.
- Once the stake period has expired, the `completeStake` method can be called by anyone, whether that be the exchange or the user.  But this method can **only** transfer the staked tokens back to the original staking address.

The following items are not implemented in the smart contract, but calculated and managed by the Nash exchange matching engine:
- Calculation of fee rewards.
- Distribution of fee rewards.

Further information about the calculation of staking dividends can be found in section 4.2.1 of [the Nash whitepaper](https://nash.io/pdfs/whitepaper_v2.pdf).

## Installation

### System Requirements

You need Python 3 (3.7 or 3.6).

OSX

    brew install python

Debian/Ubuntu 16.10+

    sudo apt-get install python3.7 python3.7-dev python3.7-venv python3-pip

### Project Setup

Clone the repository and navigate into the project directory.
Make a Python 3 virtual environment and activate it via

```shell
python3 -m venv venv
source venv/bin/activate
```

Then install the requirements via

```shell
(venv) pip install -r requirements.txt
```

## Compilation / Build

The smart contract can be compiled from the Python shell as follows:

```python
from boa.compiler import Compiler

Compiler.load_and_save('NashStaking.py')
```

This will compile the contract to `NashStaking.avm`


## Bug Reporting

Please contact us at bugbounty@neonexchange.org if you find something you believe we should know about.
