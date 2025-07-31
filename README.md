<h1 align="center">Web3 Data Lake</h1>
<p align="center">
  <img src="https://img.shields.io/badge/version-0.1.0-brightgreen.svg" alt="version">
  <a href="https://t.me/web3datalake">
    <img src="https://img.shields.io/badge/Telegram-Contact%20Us-blue?logo=telegram" alt="Telegram">
  </a>
</p>
<p align="center"><strong>Fast, cost-effective access to Ethereum Virtual Machine (EVM) blockchain data.</strong></p>

# Introduction

The Web3 Data Lake is for developers who need reliable access to **historical** and **real-time** blockchain data.

- **Fast, reliable indexing.** Use it as a high performance data source for your indexers to process.
- **Power your backend**. Access terabytes of blockchain data without worrying about hosting and maintaining infrastructure.

**Better than using an RPC node**

- **Higher throughput.** Process historical data faster than using an RPC.
- **Fewer errors.** Avoid having to make millions of fragile RPC calls when backfilling or indexing.
- **Simpler workflows.** Stream raw data directly without managing complex batching or retries.

## Overview

<table>
  <tr>
    <td align="center" width="33%">
      <a href="#getting-started"><strong>🚀 Getting Started</strong></a>
    </td>
    <td align="center" width="33%">
      <a href="#examples"><strong>📂 Examples</strong></a>
    </td>
    <td align="center" width="33%">
      <a href="#authentication"><strong>🔑 Authentication</strong></a>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="#rate-limits"><strong>📈 Rate Limits</strong></a>
    </td>
    <td align="center">
      <a href="#data-tables"><strong>🗂️ Data Tables</strong></a><br>
      <a href="#blocks">Blocks</a>, <a href="#receipts">Receipts</a>
    </td>
    <td align="center">
      <a href="#supported-chains"><strong>🌐 Supported Chains</strong></a>
    </td>
  </tr>
  <tr>
    <td align="center">
      <a href="#data-access"><strong>📦 Data Access</strong></a><br>
      <a href="#by-fetching">By Fetching</a>, <a href="#by-subscribing">By Subscribing</a>
    </td>
    <td align="center">
      <a href="#apis"><strong>🔌 APIs</strong></a><br>
      <a href="#fetch-api">Fetch API</a>, <a href="#stream-api">Stream API</a>
    </td>
    <td align="center">
      <!-- Empty or reserved for future -->
    </td>
  </tr>
</table>

## Getting Started

**What data do you provide?**

We provide complete historical coverage for **blocks**, **receipts**, and **traces**. All data is delivered in raw, unprocessed format. The same as you would receive from an RPC node.

For more details and examples, see the [**Data Tables**](#data-tables) section.

**How to access the data?**

There are two ways to access data:

- [**Fetch API**](#fetch-api) – For pull-based (on-demand) data retrieval.
- [**Stream API**](#stream-api) – For push-based (real-time) data delivery.

If you want to listen for new data in real time or download large amounts of data quickly, use the [**Stream API**](#stream-api).

To use the APIs you need an **API key**.

**How to get an API key?**

To generate a **free** API key use our [**authentication bot**](https://t.me/web3datalake_auth_bot). If you want to upgrade your API key contact our **admin**.

## Examples

| **API**       | **Example**                                                                                                                                                  |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Fetch API    | [Get all Ethereum receipts at block 1,000,000](examples/fetch-api/README.md#get-all-ethereum-receipts-at-block-1000000)<br>                                   |
|               | [Get all Ethereum receipts between block 1,000,000 and 1,000,010](examples/fetch-api/README.md#get-all-ethereum-receipts-between-block-1000000-and-1000010) |
|               | [Get all Base blocks between block 1,000,000 and 1,000,010](examples/fetch-api/README.md#get-all-base-blocks-between-block-1000000-and-10000010)           |
| Stream API | [Download all Ethereum blocks](https://github.com/web3dl/stream-api-starter#readme)                                                              |

## Authentication

#### How to get an API key?

To generate a **free** API key use our [**authentication bot**](https://t.me/web3datalake_auth_bot). If you want to upgrade your API key contact our **admin**.
#### How to use the API key?

Include your API key with every request. You can provide your API as a query parameter or in the header of your request.

- **Query parameter:** `apikey=YOUR_API_KEY`
- **Header:** `apikey: YOUR_API_KEY`

| API Type   | Query Parameter Example                                             | Header Example Command                                                           |
| ---------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Fetch API  | `https://api.web3dl.com/fetch/<chain>/<table>?apikey=YOUR_API_KEY`  | `curl -H "apikey: YOUR_API_KEY" "https://api.web3dl.com/fetch/<chain>/<table>"`  |
| Stream API | `https://api.web3dl.com/stream/<chain>/<table>?apikey=YOUR_API_KEY` | `curl -H "apikey: YOUR_API_KEY" "https://api.web3dl.com/stream/<chain>/<table>"` |


## Rate Limits

Free API keys have usage limits for both requests and data volume. For higher or **unlimited** limits, [contact us on Telegram](https://t.me/web3datalake) to upgrade your API key.

**Fetch API Limits**

| Limit Type         | Per Second           | Per Day   | Per Month |
| ------------------ | -------------------- | --------- | --------- |
| **Requests**       | 5                    | 10,000    | 100,000   |
| **Blocks**         | 100                  | 200,000 | 2,000,000 |
| **Blocks/request** | 20 (max per request) | —         | —         |

**Stream API Limits**

|Limit Type|Value|
|---|---|
|**Max concurrent connections**|1|
|**GB/month**|50|

# Data Tables

**Note:** The **reference** field is the value to use for the `table` parameter in both the Filter and Stream APIs.

## Blocks

Reference: `blocks`.

| **Field**      | **Type**  | **Indexed** | **Description**                                                                                                                                                                              |
| -------------- | --------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `block_number` | `integer` | True        | The block number of the data.                                                                                                                                                                |
| `data`         | `object`  | False       | The response data of RPC method `eth_getBlockByNumber` at block `block_number`.  <br>  <br>See [example](./examples/responses/blocks.json). |

## Receipts

Reference: `receipts`.

| **Field**      | **Type**  | **Indexed** | **Description**                                                                                                                                                                                        |
| -------------- | --------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `block_number` | `integer` | True        | The block number of the data.                                                                                                                                                                          |
| `data`         | `object`  | False       | The response data of RPC method `eth_getBlockReceipts` at block number `block_number`.  <br>  <br>See [example](./examples/responses/receipts.json). |

# Supported Chains

The tables below show which chains are currently supported for each data type.

✅ = Supported  ❌ = Not supported

| Chain    | Receipts | Blocks | Traces |
| -------- | -------- | ------ | ------ |
| Ethereum | ✅        | ✅      | ❌      |
| Base     | ✅        | ✅      | ❌      |
| Arbitrum | ✅        | ✅      | ❌      |

**Note:** Support is for full historical coverage in raw format, matching what you’d get from an RPC node.

[**Contact us**](https://t.me/web3datalake) if you need support for a chain not listed here.

#### References

Use the following slugs in your API calls to reference each table:  
`/<chain>/<table>`

| Chain    | Receipts             | Blocks             | Traces             |
| -------- | -------------------- | ------------------ | ------------------ |
| Ethereum | `/eth/receipts` | `/eth/blocks` | `/eth/traces` |
| Base     | `/base/receipts`     | `/base/blocks`     | `/base/traces`     |
| Arbitrum | `/arb/receipts` | `/arb/blocks` | `/arb/traces` |

# Data Access

There are two ways you can retrieve data. The best way depends on your use case.

- **By fetching (pull-based)**. Fetch data at a specific block or block range.
- **By subscribing (push-based)**. Open a stream and receive data continuously in sequence. This includes both historical data as well as new data as it becomes available.

## By Fetching

See [**Fetch API**](#fetch-api).

**Best for**:

- Simple on-demand queries.
- Fetching data at a specific block or small block range.

## By Subscribing

See [**Stream API**](#stream-api).

**Best for:**

- Receiving new data in real time.
- **Backfilling:** Efficiently retrieving large volumes of historical data to fill gaps or build a complete dataset (fastest method).
- **Indexing:** Providing a raw, continuous data feed for indexing or other downstream processing

# APIs

## Fetch API

**Method**: `GET`

**Endpoint**: `https://api.web3dl.com/fetch/<chain>/<table>`

### Request Parameters

| **Name**           | **Type**  | **Description**                                                                                      |
| ------------------ | --------- | ---------------------------------------------------------------------------------------------------- |
| `eq:block_number`  | `integer` | Return only rows where `block_number` equals this value.                                             |
| `lte:block_number` | `integer` | Return rows with `block_number` less than or equal to this value.                                    |
| `gte:block_number` | `integer` | Return rows with `block_number` greater than or equal to this value.                                 |
| `size`             | `integer` | Maximum number of rows to return.                                                                    |
| `order`            | `string`  | Sort order. Use `asc` for ascending or `desc` for descending by `block_number`.                      |
| `format`           | `string`  | Controls the response format. Accepted values: `json` (default) or `bytes` (lz4‑compressed payload). |

### Response


| **Field**      | **Type**                  | **Description**                                                                                                                                                                                                                                                                                                      |
| -------------- | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `block_number` | `integer`                 | The block number of the data.                                                                                                                                                                                                                                                                                        |
| `data`         | `object` <br><br><br><br> | The data corresponding to the block. The content of `data` depends on the table queried (e.g. `receipts` or `blocks`).<br><br>See [Data Tables](#data-tables) section for examples.<br><br>If `format=bytes` then `data` is a compressed binary blob which you need to decode. See [Decoding data](#decoding-data). |

## Stream API

**Method**: `GET`

**Endpoint**: `https://api.web3dl.com/stream/<chain>/<table>`

### Request Parameters

| **Name**           | **Type**  | **Description**                                                                                      |
| ------------------ | --------- | ---------------------------------------------------------------------------------------------------- |
| `lte:block_number` | `integer` | Return rows with `block_number` less than or equal to this value.                                    |
| `gte:block_number` | `integer` | Return rows with `block_number` greater than or equal to this value.                                 |


### Response

The Stream API responds with a continuous binary stream of records (`Content-Type: application/octet-stream`). Each record follows a simple binary protocol:

**Record Format**

Each streamed record follows this structure:

| **Offset** | **Length** | **Type** | **Description**                         |
| ---------- | ---------- | -------- | --------------------------------------- |
| 0          | 4 bytes    | `uint32` | Block number (big-endian)               |
| 4          | 4 bytes    | `uint32` | Length of the data payload (big-endian) |
| 8          | N bytes    | `bytes`  | Data payload (e.g., encoded JSON)       |

**Notes**

- You are expected to decode the bytes payload to access the data.
- The stream ends automatically after the `until_block` is reached.
- If `until_block` is not provided, the stream continues as new blocks arrive (i.e., tailing mode).

### Decoding `data`

The `data` field in each record is a compressed binary blob. To decode it:

1. **Decompress** the byte stream using an `lz4` decompression library.
2. **Deserialize** the decompressed bytes with `pickle` to get the original Python object.

Example:

```
import lz4.frame
import pickle

# `compressed_data` is the raw bytes you got from the API

# Step 1: Decompress with lz4
decompressed_bytes = lz4.frame.decompress(compressed_data)

# Step 2: Deserialize with pickle
original_object = pickle.loads(decompressed_bytes)
```