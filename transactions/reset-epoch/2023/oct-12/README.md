# Reset Epoch

> Oct 12th, 2023

Any time the network is sporked, the protocol state is manually initialized via the bootstrapping process.
Therefore, we need to re-synchronize the FlowEpoch smart contract each time the network is sporked, using the [ResetEpoch](../../../../templates/reset_epoch_with_end_staking_auction.cdc) transaction.

The ResetEpoch transaction however needs to be proposed by the staking contract account and payed by the service account.
Currently, the [multi-sign vercel app](https://flow-multisig-git-service-account-onflow.vercel.app/mainnet) does not support transactions with different proposer and payer hence we have to execute this via the old method using the flow-cli.

## Sequence of signing: 
1. Vishal generates the Tx
2. Round one - Signing for staking account
   1. Josh signs with flow-staking.json
   2. Find Signs with flow-staking.json
   3. Sean Signs with flow-staking.json
   4. Vishal Signs with flow-staking.json
3. Roune two - - Signing for service account
   1. Josh signs with flow.json
   2. Find Signs with flow.json
   3. Sean Signs with flow.json
   4. Vishal Signs with flow.json
4. Vishal submits the transaction

## Prerequisites
1. Latest version of the [flow-cli](https://developers.flow.com/tools/flow-cli).
2. [Gcloud cli](https://cloud.google.com/sdk/docs/install)
3. Contributor privilege to this repo.
4. Checkout this repo locally.
5. Open a terminal and go into the directory `service-account`

## Dapper Labs Builds

```sh
flow transactions build ./templates/reset_epoch_with_end_staking_auction.cdc \
  --config-path flow-staking.json \
  --network mainnet \
  --args-json "$(cat "./transactions/reset-epoch/2023/oct-12/arguments.json")" \
  --proposer 0x8624b52f9ddcd04a \
  --proposer-key-index 5 \
  --authorizer 0x8624b52f9ddcd04a \
  --payer 0xe467b9dd11fa00df \
  --gas-limit 10000000 \
  -x payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-unsigned.rlp
```

## Staking Account

## Josh Signs

Pull the transaction from git
```sh
git pull
```

Sign the transaction using Google Auth
```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-unsigned.rlp \
  --config-path flow-staking.json \
  --signer josh \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-1.rlp
```

Push the vote to git
```sh
git add .;git commit -m "reset epoch transaction for oct-12";git push origin main
```

## Find Signs

Pull the transaction from git
```sh
git pull
```

Sign the transaction using Google Auth
```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-1.rlp \
  --config-path flow-staking.json \
  --signer Find \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-2.rlp
```

Push the vote to git
```sh
git add .;git commit -m "reset epoch transaction for oct-12";git push origin main
```

## Sean Signs

Pull the transaction from git
```sh
git pull
```

Sign the transaction using Google Auth
```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-2.rlp \
  --config-path flow-staking.json \
  --signer animoca \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-3.rlp
```

Push the vote to git
```sh
git add .;git commit -m "reset epoch transaction for oct-12";git push origin main
```

## Vishal Signs

Pull the transaction from git
```sh
git pull
```

Sign the transaction using Google Auth
```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-3.rlp \
  --config-path flow-staking.json \
  --signer vishal \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-4.rlp
```

Push the vote to git
```sh
git add .;git commit -m "reset epoch transaction for oct-12";git push origin main
```

---

## Service Account
## Josh Signs

Pull the transaction from git
```sh
git pull
```

Sign the transaction using Google Auth
```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-4.rlp \
  --config-path flow.json \
  --signer josh \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-5.rlp
```

Push the vote to git
```sh
git add .;git commit -m "reset epoch transaction for oct-12";git push origin main
```

## Find Signs

Pull the transaction from git
```sh
git pull
```

Sign the transaction using Google Auth
```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-5.rlp \
  --config-path flow.json \
  --signer Find \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-6.rlp
```


Push the vote to git
```sh
git add .;git commit -m "reset epoch transaction for oct-12";git push origin main
```

## Sean Signs

```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-6.rlp \
  --config-path flow.json \
  --signer animoca \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-7.rlp
```

Push the vote to git
```sh
git add .;git commit -m "reset epoch transaction for oct-12";git push origin main
```

## Vishal Signs

Pull the transaction from git
```sh
git pull
```

Sign the transaction using Google Auth
```sh
flow transactions sign ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-7.rlp \
  --config-path flow.json \
  --signer vishal \
  --filter payload \
  --save ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-complete.rlp
```

## Vishal Submits

```sh
flow transactions send-signed --network mainnet ./transactions/reset-epoch/2023/oct-12/reset-epoch-oct-12-sig-complete.rlp
```

## Results

Succeeded:
https://flowscan.org/transaction/


