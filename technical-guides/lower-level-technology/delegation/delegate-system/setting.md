---
description: Here we will cover the delegation activation setting
---

# Setting

## Set the .env delegation variable

```shell
# ========== DELEGATION ==============
## Active the delegate feature for service / proposal / release / review (the proposal validation won't be delegate)
NEXT_PUBLIC_ACTIVE_DELEGATE=true

## Active the delegate feature for minting ID - will call a backend api and call the smartcontract function mintForAddress
NEXT_PUBLIC_ACTIVE_DELEGATE_MINT=true

## This seed phrase is only used for delegate purpose
NEXT_PRIVATE_DELEGATE_SEED_PHRASE="add you seed phrase here only for delegate purpose"

## Public address
NEXT_PUBLIC_DELEGATE_ADDRESS="0xaddyouraddresshereonlyfordelegatepurpose"
```



```sh
NEXT_PUBLIC_ACTIVE_DELEGATE=true
```

The `NEXT_PUBLIC_ACTIVE_DELEGATE` variable will display the activation button in the settings dashboard, allowing users to activate and deactivate the delegation feature.

```sh
NEXT_PUBLIC_ACTIVE_DELEGATE_MINT=true
```

The `NEXT_PUBLIC_ACTIVE_DELEGATE_MINT` variable will enable users to mint their TalentLayerID without incurring any fees.

```sh
NEXT_PRIVATE_DELEGATE_SEED_PHRASE="add you seed phrase here only for delegate purpose"
```

The `NEXT_PRIVATE_DELEGATE_SEED_PHRASE` is required to pay the fees for the user's actions. The wallet should be used exclusively for delegation purposes.

```sh
NEXT_PUBLIC_DELEGATE_ADDRESS="0xaddyouraddresshereonlyfordelegatepurpose"
```

The NEXT\_PUBLIC\_DELEGATE\_ADDRESS is the public address used for transactions.
