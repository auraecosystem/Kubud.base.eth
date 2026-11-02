eth_accounts

---
updatedAt: 2025-09-18T22:18:54.000Z
agentTools:
  projectIndex: https://nodereal.readme.io/llms.txt
---

# eth_accounts

Returns a list of addresses owned by client.

> 📘 Supported on both BNB Smart Chain and opBNB Chain.

The format of a BNB Smart Chain endpoint:\
`https://bsc-mainnet.nodereal.io/v1/{{apiKey}}`

`https://bsc-testnet.nodereal.io/v1/{{apiKey}}`

The format of an opBNB Chain endpoint:

`https://opbnb-testnet.nodereal.io/v1/{{apiKey}}`

# OpenAPI definition

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "Account Information",
    "version": "1.0"
  },
  "servers": [
    {
      "url": "https://bsc-mainnet.nodereal.io/v1"
    }
  ],
  "paths": {
    "/{apiKey}": {
      "post": {
        "summary": "eth_accounts",
        "description": "Returns a list of addresses owned by client.",
        "tags": [],
        "parameters": [
          {
            "name": "apiKey",
            "in": "path",
            "schema": {
              "type": "string",
              "default": "64a9df0874fb4a93b9d0a3849de012d3"
            },
            "required": true
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "allOf": [
                  {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "integer",
                        "default": 1
                      },
                      "jsonrpc": {
                        "type": "string",
                        "default": "2.0"
                      }
                    }
                  },
                  {
                    "type": "object",
                    "properties": {
                      "method": {
                        "type": "string",
                        "default": "eth_accounts",
                        "enum": [
                          "eth_accounts"
                        ]
                      }
                    }
                  }
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Returns 20 Bytes - addresses owned by the client.",
            "content": {
              "application/json": {
                "schema": {
                  "allOf": [
                    {
                      "type": "object",
                      "properties": {
                        "id": {
                          "type": "integer"
                        },
                        "jsonrpc": {
                          "type": "string"
                        }
                      }
                    },
                    {
                      "type": "object",
                      "properties": {
                        "result": {
                          "type": "string"
                        }
                      }
                    }
                  ]
                }
              }
            }
          }
        },
        "operationId": "eth-accounts"
      }
    }
  },
  "x-readme": {
    "explorer-enabled": true,
    "proxy-enabled": true
  }
}
```
