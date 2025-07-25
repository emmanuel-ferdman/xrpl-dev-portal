---
html: xchaincreateclaimid.html 
parent: transaction-types.html
seo:
    description: Create a cross-chain claim ID that is used for a cross-chain transfer.
labels:
  - Interoperability
status: not_enabled
---
# XChainCreateClaimID
[[Source]](https://github.com/XRPLF/rippled/blob/1e01cd34f7a216092ed779f291b43324c167167a/src/xrpld/app/tx/detail/XChainBridge.h#L141-L158 "Source")

_(Requires the [XChainBridge amendment][] {% not-enabled /%})_

The `XChainCreateClaimID` transaction creates a new cross-chain claim ID that is used for a cross-chain transfer. A cross-chain claim ID represents *one* cross-chain transfer of value. 

This transaction is the first step of a cross-chain transfer of value and is submitted on the destination chain, not the source chain. 

It also includes the account on the source chain that locks or burns the funds on the source chain.


## Example XChainCreateClaimID JSON

```json
{
  "Account": "rahDmoXrtPdh7sUdrPjini3gcnTVYjbjjw",
  "OtherChainSource": "rMTi57fNy2UkUb4RcdoUeJm7gjxVQvxzUo",
  "TransactionType": "XChainCreateClaimID",
  "SignatureReward": "100",
  "XChainBridge": {
    "LockingChainDoor": "rMAXACCrp3Y8PpswXcg3bKggHX76V3F8M4",
    "LockingChainIssue": {
      "currency": "XRP"
    },
    "IssuingChainDoor": "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
    "IssuingChainIssue": {
      "currency": "XRP"
    }
  }
}
```


## XChainCreateClaimID Fields

| Field              | JSON Type            | [Internal Type][] | Required? | Description |
|:-------------------|:---------------------|:------------------|:----------|-------------|
| `OtherChainSource` | String - [Address][] | AccountID         | Yes       | The account that must send the `XChainCommit` transaction on the source chain. |
| `SignatureReward`  | [Currency Amount][]  | Amount            | Yes       | The amount, in XRP, to reward the witness servers for providing signatures. This must match the amount on the `Bridge` ledger object. |
| `XChainBridge`     | XChainBridge         | XChainBridge      | Yes       | The bridge to create the claim ID for. |


### XChainBridge Fields

| Field               | JSON Type | [Internal Type][] | Required? | Description     |
|:--------------------|:----------|:------------------|:----------|:----------------|
| `IssuingChainDoor`  | String    | Account           | Yes       | The door account on the issuing chain. For an XRP-XRP bridge, this must be the genesis account (the account that is created when the network is first started, which contains all of the XRP). |
| `IssuingChainIssue` | Issue     | Issue             | Yes       | The asset that is minted and burned on the issuing chain. For an IOU-IOU bridge, the issuer of the asset must be the door account on the issuing chain, to avoid supply issues. |
| `LockingChainDoor`  | String    | Account           | Yes       | The door account on the locking chain. |
| `LockingChainIssue` | Issue     | Issue             | Yes       | The asset that is locked and unlocked on the locking chain. |

{% raw-partial file="/docs/_snippets/common-links.md" /%}
