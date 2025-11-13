---
hide:
  - navigation
---

# Raredex Python SDK

!!! warning
    **Experimental SDK, library API is subject to change**

::: raredex_py.raredex.Raredex
    handler: python
    options:
      show_source: false
      show_root_heading: true

## L2-Only Authentication (Subkeys)

For users who only have L2 credentials (subkeys) and don't need L1 onboarding:

::: raredex_py.raredex_subkey.RaredexSubkey
    handler: python
    options:
      show_source: false
      show_root_heading: true

### Usage Examples

**L1 + L2 Authentication (Traditional):**
```python
from raredex_py import Raredex
from raredex_py.environment import Environment

# Requires both L1 and L2 credentials
raredex = Raredex(
    env=Environment.TESTNET,
    l1_address="0x...",
    l1_private_key="0x..."
)
```

**L2-Only Authentication (Subkeys):**
```python
from raredex_py import RaredexSubkey
from raredex_py.environment import Environment

# Only requires L2 credentials - no L1 needed
raredex = RaredexSubkey(
    env=Environment.TESTNET,
    l2_private_key="0x...",
    l2_address="0x..."
)

# Use exactly like regular Paradex
await raredex.init_account()  # Already initialized
markets = await raredex.api_client.get_markets()
```

**WebSocket Usage:**
```python
async def on_message(ws_channel, message):
    print(ws_channel, message)

await raredex.ws_client.connect()
await raredex.ws_client.subscribe(RaredexWebsocketChannel.MARKETS_SUMMARY, callback=on_message)
```

### When to Use Each Approach

**Use `Raredex` (L1 + L2) when:**
- You have both L1 (Ethereum) and L2 (Starknet) credentials
- You have never logged in to Raredex using this account before
- You need to perform on-chain operations (transfers, withdrawals)

**Use `RaredexSubkey` (L2-only) when:**
- You only have L2 credentials
- The account has already been onboarded (You have logged in to Raredex before)
- You do not need on-chain operations (withdrawals, transfers)

### Key Differences

| Feature | `Raredex` | `RaredexSubkey` |
|---------|-----------|-----------------|
| **Authentication** | L1 + L2 | L2-only |
| **Onboarding** | ✅ Supported | ❌ Blocked |
| **On-chain Operations** | ✅ Supported | ❌ Blocked |
| **API Access** | ✅ Full access | ✅ Full access |
| **WebSocket** | ✅ Supported | ✅ Supported |
| **Order Management** | ✅ Supported | ✅ Supported |

## API Documentation Links

Full details for REST API & WebSocket JSON-RPC API can be found at the following links:

- [Environment - Testnet](https://docs.api.testnet.raredex.trade){:target="_blank"}
- [Environment - Prod](https://docs.api.prod.raredex.trade){:target="_blank"}

::: raredex_py.api.api_client.RaredexApiClient
    handler: python
    options:
      show_source: false
      show_root_heading: true

::: raredex_py.api.ws_client.RaredexWebsocketChannel
    handler: python
    options:
      show_source: false
      show_root_heading: true

::: raredex_py.api.ws_client.RaredexWebsocketClient
    handler: python
    options:
      show_source: false
      show_root_heading: true

::: raredex_py.account.account.RaredexAccount
    handler: python
    options:
      show_source: false
      show_root_heading: true

::: raredex_py.account.subkey_account.SubkeyAccount
    handler: python
    options:
      show_source: false
      show_root_heading: true
