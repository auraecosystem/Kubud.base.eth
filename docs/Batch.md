Batch Requests

---
updatedAt: 2025-09-18T22:18:53.000Z
agentTools:
  projectIndex: https://nodereal.readme.io/llms.txt
---

# Batch Requests

You can send multiple requests within one batch call in MegaNode. This
  document explains how to send it and its limitation.

## What are "Batch Requests"?

In some practices, you need to send multiple API calls to get what you need. You can either send  API requests multiple times, or simply send multiple API calls nested in a single HTTP request. The latter is "Batch Requests"

However, we do not recommend using batch requests since the nature of batch requests may not have the same reliability as single requests, especially when you have too many requests in a single call.

## **Who is allowed to send batch requests?**

All MegaNode users, regardless of your pricing plan, are allowed to send batch requests.

## Batch requests limitation

You can send batch requests only if the API calls nested within it are no more than 500 requests. Also, you can't send debug API requests as part of your batch request.

## **How do batch requests cost?**

The cost of batch requests is according to the API calls nested within it. For example, if you send a batch request and there're 4 *eth\_blockNumber* calls inside, it costs total CUs in total.

## Example (HTTPs)

**Request**

```cURL
curl https://bsc-mainnet.nodereal.io/v1/your-api-key \
-X POST \
-H "Content-Type: application/json" \
-d '[{"jsonrpc": "2.0", "id": 1, "method": "eth_blockNumber", "params": []},
{"jsonrpc": "2.0", "id": 2, "method": "eth_blockNumber", "params": []},
{"jsonrpc": "2.0", "id": 3, "method": "eth_blockNumber", "params": []},
{"jsonrpc": "2.0", "id": 4, "method": "eth_blockNumber", "params": []}]'
```

**Result**

```txt
[{"jsonrpc":"2.0","id":1,"result":"0x12eed11"},{"jsonrpc":"2.0","id":2,"result":"0x12eed11"},{"jsonrpc":"2.0","id":3,"result":"0x12eed11"},{"jsonrpc":"2.0","id":4,"result":"0x12eed11"}]
```

## Example (WSS)

Currently, you can only make batch request via WSS on [Arbitrum Nitro](https://nodereal.io/api-marketplace/arbitrum-nitro-rpc), [Arbitrum Nova](https://nodereal.io/api-marketplace/arbitrum-nova-rpc) and [Avalanche C-Chain](https://nodereal.io/api-marketplace/avalanche-c).

**Request**

```bash
$ wscat -c wss://open-platform.nodereal.io/ws/{{apiKey}}/arbitrum-nitro/

// Send batch request:
> [{"method":"eth_getBlockByNumber","params":["0xc5043f",false],"id":1,"jsonrpc":"2.0"},    {"method": "eth_chainId","params": [],"id": 1,"jsonrpc": "2.0"}]
```

**Result**

```txt
< [{"jsonrpc":"2.0","id":1,"result":{"difficulty":"0x0","extraData":"0x","gasLimit":"0xbc87657","gasUsed":"0x3daa0","hash":"0x8f9ecad637559914862de6821bd352d6ac7744d130085d4c5b3d821786aab3ac","l1BlockNumber":"0xe2733e","logsBloom":"0x00080000000000000080000000000010000000000000000000020000000000000000000000000080000000000000004400000000000004000000000000800000000000000000008000000000000000000000000000000000200000000000000000080000000000000000000000000000000000000000000000040000000000080000000000004008004000000000000000800000000000000000000000000000000000000000000000000000040000000000000000004000000000000004000000000000000000000000000000000000000000004000000000000000000000000008000000000010000400000000020000000000000000000000000020000000","miner":"0x0000000000000000000000000000000000000000","mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000","nonce":"0x0000000000000000","number":"0xc5043f","parentHash":"0xf1b5d6a7a45df869b2eef85541584c69bbeb7a58f77e557d4898de2b464d5715","receiptsRoot":"0x17f8ad0067aff1dbb35d5100b1f131838564b3e980e2b8a2674b8d5362d12e97","sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347","size":"0x367","stateRoot":"0x0000000000000000000000000000000000000000000000000000000000000000","timestamp":"0x628dde24","totalDifficulty":"0x0","transactions":["0x39229c9c973b7675086e4404c30fd23b4130bdb33cef8f799ac0450e2489ba08"],"transactionsRoot":"0xc4b4888ec249430e95f700432d21a3042e5dd2572e68771dc61f73e1fbbd9900","uncles":[]}},{"jsonrpc":"2.0","id":1,"result":"0xa4b1"}]
```
