# TalentLayerID.sol

****[**TalentLayerID.sol**](https://github.com/TalentLayer/talentlayer-id-contracts/blob/main/contracts/TalentLayerID.sol) is the smart contract that initializes a user's TalentLayer ID. The contract can be used to:

* Mint a TalentLayer ID
* Link Proof of Humanity to your TalentLayerID
* Initiate account recovery process
* Look up TalentLayer users or their handles

## Structure

### Mappings

{% code lineNumbers="true" %}
```solidity
mapping(uint256 => Profile) public profiles;
```
{% endcode %}

### On-chain data

{% code lineNumbers="true" %}
```solidity
struct Profile {
    uint256 id;
    string handle;
    address pohAddress;
    uint256 platformId;
    string dataUri; 
}
```
{% endcode %}

## Functions

### Minting

{% hint style="info" %}
Minting a [TalentLayerID](../../basics/readme/what-is-talentlayer-id.md#what-is-a-talentlayerid) requires a [PlatformID](../../basics/elements/platformid.md).&#x20;
{% endhint %}

There are two ways to mint a TalentLayerID, one that requires that the owner of the wallet address is registered with [Proof of Humanity](https://www.proofofhumanity.id/), and one that does not. [PoH](https://www.proofofhumanity.id/) is the system currently used in talentlayer for [sybil resistance](https://en.wikipedia.org/wiki/Sybil\_attack).&#x20;

Only one TalentLayerID can be minted per address.&#x20;

#### The Simple Way

{% code lineNumbers="true" %}
```solidity
function mint(uint256 _platformId, string memory _handle) public canMint(_handle, _platformId)
```
{% endcode %}

#### Proof of Humanity (PoH)

A user needs to get their wallet address registered with [Proof of Humanity](https://www.proofofhumanity.id/) before linking it to their [TalentLayerID](../../basics/readme/what-is-talentlayer-id.md).&#x20;

{% code overflow="wrap" lineNumbers="true" %}
```solidity
function mintWithPoh(uint256 _platformId, string memory _handle) public canMint(_handle, _platformId);
```
{% endcode %}

If [a TalentLayerID has been minted without Proof of Humanity](talentlayerid.sol.md#the-simple-way) and the user wants to link their TalentLayerID to proof of humanity, then that can also be achieved.

{% code lineNumbers="true" %}
```solidity
function isTokenPohRegistered(uint256 _tokenId) public view returns (bool);
function activatePoh(uint256 _tokenId) public;
```
{% endcode %}

### Account Recovery

Recovering an account allows moving a [TalentLayerID](../../basics/readme/what-is-talentlayer-id.md) to a new wallet address without accessing the current one by providing a recovery key.&#x20;

{% hint style="warning" %}
2022-11-24: The recovery functionality is being audited and revised. More information will be provided shortly.
{% endhint %}

{% code lineNumbers="true" %}
```solidity
function recoverAccount(
        address _oldAddress,
        uint256 _tokenId,
        uint256 _index,
        uint256 _recoveryKey,
        string calldata _handle,
        bytes32[] calldata _merkleProof
) public;
```
{% endcode %}

## Visualization

<figure><img src="../../.gitbook/assets/TalentLayerId.png" alt=""><figcaption><p>made with <a href="https://marketplace.visualstudio.com/items?itemName=tintinweb.solidity-visual-auditor">Solidity Visual Developer</a> plugin</p></figcaption></figure>

## Learn More

Learn more about why we have TalentLayer IDs and how they function in workflows:&#x20;

{% content-ref url="../../basics/readme/what-is-talentlayer-id.md" %}
[what-is-talentlayer-id.md](../../basics/readme/what-is-talentlayer-id.md)
{% endcontent-ref %}
