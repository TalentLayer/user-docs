# Install Contracts Locally

{% hint style="warning" %}
**ALERT:** In most cases, you don't need to set up local contracts - everything is ready to use on Testnet! If you have advanced needs, we recommend contacting our team.&#x20;
{% endhint %}

## Requirements

[Hardhat](https://hardhat.org/). Installation instructions found [here](https://hardhat.org/hardhat-runner/docs/getting-started#installation)

## Instructions

### 1. Clone Repository From GitHub

```bash
git clone https://github.com/TalentLayer/talentlayer-id-contracts.git
```

### 2. Navigate to Folder

```bash
cd talentlayer-id-contracts
```

### 3. Install Dependencies

```bash
npm install
```

### 4. Create Environment Files&#x20;

```bash
touch .env
```

{% hint style="info" %}
Setup .env according to [this example](https://github.com/TalentLayer/talentlayer-id-contracts/edit/main/.env.example).
{% endhint %}

### 5. Create A Local Hardhat Chain

```bash
npx hardhat node 
```

### 6. Deploy Contracts to Local Chain

{% hint style="info" %}
Please see ./talentlayer-id-contracts/Makefile for more details.
{% endhint %}

{% hint style="info" %}
Open up a new instance of the terminal (Mac/Linux) or command line (Windows).
{% endhint %}

```bash
make install
```

### 7. Run Tests

```bash
npx hardhat test
```
