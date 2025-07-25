---
html: checkcash.html
parent: transaction-types.html
seo:
    description: Redeem a check.
labels:
  - Checks
---
# CheckCash
[[Source]](https://github.com/XRPLF/rippled/blob/1e01cd34f7a216092ed779f291b43324c167167a/src/xrpld/app/tx/detail/CashCheck.cpp "Source")

Attempts to redeem a Check object in the ledger to receive up to the amount authorized by the corresponding [CheckCreate transaction][]. Only the `Destination` address of a Check can cash it with a CheckCash transaction. Cashing a check this way is similar to executing a [Payment][] initiated by the destination.

Since the funds for a check are not guaranteed, redeeming a Check can fail because the sender does not have a high enough balance or because there is not enough liquidity to deliver the funds. If this happens, the Check remains in the ledger and the destination can try to cash it again later, or for a different amount.

_(Added by the [Checks amendment][].)_

## Example {% $frontmatter.seo.title %} JSON

```json
{
    "Account": "rfkE1aSy9G8Upk4JssnwBxhEv5p4mn2KTy",
    "TransactionType": "CheckCash",
    "Amount": "100000000",
    "CheckID": "838766BA2B995C00744175F69A1B11E32C3DBC40E64801A4056FCBD657F57334",
    "Fee": "12"
}
```

{% tx-example txid="67B71B13601CDA5402920691841AC27A156463678E106FABD45357175F9FF406" /%}


{% raw-partial file="/docs/_snippets/tx-fields-intro.md" /%}

| Field        | JSON Type           | [Internal Type][] | Description         |
|:-------------|:--------------------|:------------------|:--------------------|
| `CheckID`    | String              | UInt256           | The ID of the [Check ledger object](../../ledger-data/ledger-entry-types/check.md) to cash, as a 64-character hexadecimal string. |
| `Amount`     | [Currency Amount][] | Amount            | _(Optional)_ Redeem the Check for exactly this amount, if possible. The currency must match that of the `SendMax` of the corresponding CheckCreate transaction. You must provide either this field or `DeliverMin`. |
| `DeliverMin` | [Currency Amount][] | Amount            | _(Optional)_ Redeem the Check for at least this amount and for as much as possible. The currency must match that of the `SendMax` of the corresponding CheckCreate transaction. You must provide either this field or `Amount`. |

The transaction ***must*** include either `Amount` or `DeliverMin`, but not both.

## Error Cases

- If the sender of the CheckCash transaction is not the `Destination` of the check, the transaction fails with the result code `tecNO_PERMISSION`.
- If the Check identified by the `CheckID` field does not exist, the transaction fails with the result `tecNO_ENTRY`.
- If the Check identified by the `CheckID` field has already expired, the transaction fails with the result `tecEXPIRED`.
- If the destination of the Check has the `RequireDest` flag enabled but the Check, as created, does not have a destination tag, the transaction fails with the result code `tecDST_TAG_NEEDED`.
- If the transaction specifies both `Amount` and `DeliverMin`, or omits both, the transaction fails with the result `temMALFORMED`.
- If the `Amount` or `DeliverMin` does not match the currency (and issuer, if not XRP) of the Check, the transaction fails with the result `temBAD_CURRENCY`.

{% raw-partial file="/docs/_snippets/common-links.md" /%}
