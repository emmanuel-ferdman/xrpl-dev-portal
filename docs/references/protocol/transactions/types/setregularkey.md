---
html: setregularkey.html
parent: transaction-types.html
seo:
    description: Add, remove, or modify an account's regular key pair.
labels:
  - Security
---
# SetRegularKey

[[Source]](https://github.com/XRPLF/rippled/blob/1e01cd34f7a216092ed779f291b43324c167167a/src/xrpld/app/tx/detail/SetRegularKey.cpp "Source")

A `SetRegularKey` transaction assigns, changes, or removes the regular key pair associated with an account.

You can protect your account by assigning a regular key pair to it and using it instead of the master key pair to sign transactions whenever possible. If your regular key pair is compromised, but your master key pair is not, you can use a `SetRegularKey` transaction to regain control of your account.

## Example {% $frontmatter.seo.title %} JSON

```json
{
    "Flags": 0,
    "TransactionType": "SetRegularKey",
    "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
    "Fee": "12",
    "RegularKey": "rAR8rR8sUkBoCZFawhkWzY4Y5YoyuznwD"
}
```

{% tx-example txid="6AA6F6EAAAB56E65F7F738A9A2A8A7525439D65BA990E9BA08F6F4B1C2D349B4" /%}

{% raw-partial file="/docs/_snippets/tx-fields-intro.md" /%}
<!--{# fix md highlighting_ #}-->

| Field        | JSON Type | [Internal Type][] | Description                   |
|:-------------|:----------|:------------------|:------------------------------|
| `RegularKey` | String    | AccountID         | _(Optional)_ A base-58-encoded [Address][] that indicates the regular key pair to be assigned to the account. If omitted, removes any existing regular key pair from the account. Must not match the master key pair for the address. |

## See Also

For more information about regular and master key pairs, see [Cryptographic Keys](../../../../concepts/accounts/cryptographic-keys.md).

For a tutorial on assigning a regular key pair to an account, see [Working with a Regular Key Pair](../../../../tutorials/how-tos/manage-account-settings/assign-a-regular-key-pair.md).

For even greater security, you can use [multi-signing](../../../../concepts/accounts/multi-signing.md), but multi-signing requires additional XRP for the [transaction cost][] and [reserve](../../../../concepts/accounts/reserves.md).

{% raw-partial file="/docs/_snippets/common-links.md" /%}
