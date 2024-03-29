# TVC Governance Vote

Developed by Zantetsu from Shinobi Systems, [Timely Vote Credots](https://docs.solanalabs.com/proposals/timely-vote-credits) has been [proposed](https://forum.solana.com/t/proposal-for-enabling-the-timely-vote-credits-mechanism-on-solana-mainnet/1179) for governance voting.

**All relevant addresses etc shared at the bottom of this document**

The governance vote is being conducted in the following manner:

1. A discussion has taken place on the Solana Tech Discord in the #vote-timely-vote-credits channel
2. A formal proposal was posted on the Solana Forum followed by a discussion period
3. At the start of epoch 595 (28 March 2024 UTC) stake weights of all validators have been captured
   - The [SPL Feature Proposal](https://spl.solana.com/feature-proposal#feature-proposal-life-cycle) program is being used
   - The program will mint a new SPL token with a supply equal to the total active stake lamports on the network
   - The program generates a CSV file with each validator's identity public key and the number of tokens to be sent to them (equal to their active stake lamports)
   - The CSV file is shared (in this repository) together with a script that allows any user to verify its accuracy (`check_stake_weights.sh`)
4. Tokens are distributed to all validator identity accounts in epoch 596 (at approximately 1600 UTC on 31 March 2024) and distribution can be validated
5. Validators will have until the end of epoch 599 to submit their votes by transferring their vote tokens to one of three defined recipient addresses
6. At the start of epoch 600 the token balances of each account will be tallied, if the sum of YES votes is >2/3 of the sum of all YES and NO votes cast the proposal will be considered passed

## Verifying the CSV file
Please use the `check_stake_weights.sh` script to verify the CSV file against on-chain stake weight. This can only be done during epoch 595 as stake weights will change after this.

Usage:
```
bash ./check_stake_weights.sh [OPTIONAL_RPC_ADDRESS] ./feature-proposal.csv
```

Some users have reported a 1 lamport difference for the node identity `CW9C7HBwAMgqNdXkNgFg9Ujr3edR2Ab9ymEuQnVacd1A` while others report a match, this is likely a rounding issue but given the negligible impact can be accepted for this vote.

## Verifying token distribution
Immediately after token distribution takes place on Sunday 31 March 2024 at approximately 1600 UTC (will be confirmed shortly before on Discord on the #vote-timely-vote-credits channel) the balances of all accounts can be verified with the following command:

```
solana-tokens spl-token-balances --mint JgsupiMjcJgxLJfdWpYLJt3ivGdsyPuEumEYuFNDwqq --input-csv feature-proposal.csv
```

As soon as any validators move their tokens the above won't work. The distribution commands and execution will be screen recorded and uploaded to this repository as well.

## Important hashes and addresses

**Distribution CSV file hash**

Clone this repository and use the below to verify the SHA SUM of the CSV file is equal to `dcaf5c00e2b1ccf48001b7c3754bf0b87b0735dd`
```
git clone https://github.com/laine-sa/tvc-gov.git
cd tvc-gov
cat feature-proposal.csv | sort | shasum
```

**Token Mint Address**
```
JgsupiMjcJgxLJfdWpYLJt3ivGdsyPuEumEYuFNDwqq
```

**Voting Addresses**
Send tokens to these addresses to cast your vote:
```
YES 	97z9tVZayd5LKYsD5eTfWBQVGeQMiVqKxoL8izZ34TCq
NO 	BKfP2dcDkCYBxZHBgGu8VRMudrPPPA1pdigy1LqSV5W6
ABSTAIN	5TWEPR2ATiHtAQnaZKdKdBFwqCm35deqiSbkiEmyshvk
```

*Associated token accounts will be created once the token is minted and the first vote is cast to each address*
