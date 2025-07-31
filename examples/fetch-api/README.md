
# Get all Ethereum receipts at block 1000000

## Request

```
curl -X GET "https://api.web3dl.com/fetch/eth/receipts?eq:block_number=1000000&format=json&apikey=YOUR_API_KEY"
```

**Parameters**

| **Name**          | **Type** | **Value**  | **Description**                                       |
| ----------------- | -------- | ---------- | ----------------------------------------------------- |
| `chain`           | Path     | `eth`      | Blockchain identifier.                                |
| `table`           | Path     | `receipts` | Data table to query.                                  |
| `eq:block_number` | Query    | `1000000`  | Filter results where `block_number` equals `1000000`. |
| `format`          | Query    | `json`     | Output format (`json` or `bytes`).                    |
| `apikey`          | Query    | `YOUR_API_KEY` | Your API key for authentication.                  |

## Response

```
[
	{
		"block_number": 1000000,
		"data": ...
	}
]
```

The field `data` contains the response of RPC method `eth_getBlockReceipts` at block `1000000`. See [example](./responses/eth-eq-receipts.json).


# Get all Ethereum Receipts Between Block 1000000 and 1000010

## Request

```
curl -X GET "https://api.web3dl.com/fetch/eth/receipts?gte:block_number=1000000&lte:block_number=1000010&format=json&apikey=YOUR_API_KEY"
```

**Parameters**

| **Name**           | **Type** | **Value**  | **Description**                                                            |
| ------------------ | -------- | ---------- | -------------------------------------------------------------------------- |
| `chain`            | Path     | `eth`      | Blockchain identifier.                                                     |
| `table`            | Path     | `receipts` | Data table to query.                                                       |
| `gte:block_number` | Query    | `1000000`  | Filter results where `block_number` is greater than or equal to `1000000`. |
| `lte:block_number` | Query    | `1000010`  | Filter results where `block_number` is less than or equal to `1000010`.    |
| `format`           | Query    | `json`     | Output format (`json` or `bytes`).                                         |
| `apikey`           | Query    | `YOUR_API_KEY` | Your API key for authentication.                                      |

## Response

```
[
	{
		"block_number": 1000000,
		"data": ...
	},
	...
	{
		"block_number": 1000010,
		"data": ...
	}
]
```

The response is an array of objects, each with a `block_number` and corresponding `data` from RPC method `eth_getBlockReceipts` for blocks `1000000–1000010`. See [example](./responses/eth-receipts-between.json).
# Get all Base blocks between block 1000000 and 10000010

## Request

```
curl -X GET "https://api.web3dl.com/fetch/base/blocks?gte:block_number=1000000&lte:block_number=1000010&format=json&apikey=YOUR_API_KEY"
```

**Parameters**

| **Name**           | **Type** | **Value**  | **Description**                                                            |
| ------------------ | -------- | ---------- | -------------------------------------------------------------------------- |
| `chain`            | Path     | `base`     | Blockchain identifier.                                                     |
| `table`            | Path     | `blocks`   | Data table to query.                                                       |
| `gte:block_number` | Query    | `1000000`  | Filter results where `block_number` is greater than or equal to `1000000`. |
| `lte:block_number` | Query    | `1000010`  | Filter results where `block_number` is less than or equal to `1000010`.    |
| `format`           | Query    | `json`     | Output format (`json` or `bytes`).                                         |
| `apikey`           | Query    | `YOUR_API_KEY` | Your API key for authentication.                                      |

## Response

```
[
	{
		"block_number": 1000000,
		"data": ...
	},
	...
	{
		"block_number": 1000010,
		"data": ...
	}
]
```

The response is an array of objects, each with a `block_number` and corresponding `data` from RPC method `eth_getBlockByNumber` for blocks `1000000–1000010`. See [example](./responses/base-blocks-between.json).
