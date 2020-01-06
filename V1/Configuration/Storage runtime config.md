---
uid: storageruntime
---

# Storage runtime configuration

Edge Data Store provides a mechanism for configuring runtime characteristics of the storage component.  

> **Note:** The configured defaults are sufficent for most scenarios.  You should modify these values  only after consultation with OSIsoft Support personnel.

## Configure storage runtime

To update the storage runtime configuration, complete the following:

1. Create a JSON file with the storage runtime configuration.

**Note:** See the following *Parameters* table for all available runtime parameters to define.
          See the following *Examples* section for an example of a valid runtime configuration file.
          
2. Save the JSON file with the name Storage_Runtime.config.json.
3. From the same directory where the file exists, run the following curl script:

```bash
curl -i -d "@Storage_Runtime.config.json" -H "Content-Type: application/json" -X PUT http://localhost:5590/api/v1/configuration/storage/Runtime
```

> **Note:** The @ symbol is a required prefix for the above command.

### Parameters

| Parameter                       | Required | Type     | Description                                        |
|---------------------------------|----------|----------|----------------------------------------------------|
| **IngressDebugExpiration**      | Required | string   | If set, defines how long OMF ingress debug files should be produced. |
| **StreamStorageLimitMb**        | Required | integer  | The maximum size in megabytes that a stream can reach. |
| **StreamStorageTargetMb**       | Required | integer  | The size in megabytes that a stream will be reduced to after StreamStorageLimitMb size is reached for a single stream. |
| **EnableTransactionLog**        | No       | bool     | Enables or disables the transaction log.  The transaction log helps to ensure no data is lost should a device lose power. |
| **TransactionLogLimitMB**       | No       | integer  | Maximum size for transaction log file.  Transaction log files larger than this size will be deleted, resulting is loss of data should the device lose power. |
| **CheckpointRateInSec**         | No       | integer  | How often to flush new data to store.  |


### Examples

The following is a valid runtime configuration example.

```json
{
  "streamStorageLimitMb": 2,
  "streamStorageTargetMb": 1,
  "ingressDebugExpiration": "0001-01-01T00:00:00",
  "checkpointRateInSec": 30,
  "transactionLogLimitMB": 250,
  "enableTransactionLog": true
}```

## Storage runtime schema

| Abstract            | Extensible | Status       | Identifiable | Custom properties | Additional properties | Defined in                                                 |
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- | ---------------------------------------------------------- |
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             | [Storage_Runtime_schema.json](Storage_Runtime_schema.json) |

## Storage runtime configuration properties

| Property                                          | Type      | Required     | Nullable | Defined by                                |
| ------------------------------------------------- | --------- | ------------ | -------- | ----------------------------------------- |
| [IngressDebugExpiration](#ingressdebugexpiration) | `string`  | **Required** | No       | StorageRuntimeConfiguration (this schema) |
| [StreamStorageLimitMb](#streamstoragelimitmb)     | `integer` | **Required** | No       | StorageRuntimeConfiguration (this schema) |
| [StreamStorageTargetMb](#streamstoragetargetmb)   | `integer` | **Required** | No       | StorageRuntimeConfiguration (this schema) |
| [EnableTransactionLog](#enabletransactionlog)     | `bool`    | No           | No       | StorageRuntimeConfiguration (this schema) |
| [TransactionLogLimitMB](#transactionloglimitmb)   | `integer` | No           | No       | StorageRuntimeConfiguration (this schema) |
| [CheckpointRateInSec](#checkpointrateinsec)       | `integer` | No           | No       | StorageRuntimeConfiguration (this schema) |

### IngressDebugExpiration

Ingress Debug Expiration is a property that can be used when debugging OMF. If the date and time is the future incoming OMF messages will be logged until the date and time specified. Once the configured time is past OMF messages will no longer be logged for debugging purposes.

#### IngressDebugExpiration type

`string`

- format: `date-time` � date and time (according to [RFC 3339, section 5.6](http://tools.ietf.org/html/rfc3339))
- minimum length: 1 characters

### StreamStorageLimitMb

StreamStorageLimitMb is the maximum size in megabytes that a stream can reach. When a stream exceeds the size specified, older data will be deleted from the file. Data will be removed from the stream until the stream is at or below the StreamStorageTargetMb value. It is recommended that the target value be smaller than the limit since trimming can be an expensive operation and should be done infrequently.

#### StreamStorageLimitMb type

`integer`

- minimum value: `2`
- maximum value: `2147483647`

### StreamStorageTargetMb

StreamStorageTargetMb is the size in megabytes that a stream will be reduced to after StreamStorageLimitMb size is reached for a single stream. When a stream exceeds the size specified, older data will be deleted from the file. Data will be removed from the stream until the stream is at or below the StreamStorageTargetMb value. It is recommended that the target value be smaller than the limit since trimming can be an expensive operation and should be done infrequently.

#### StreamStorageTargetMb type

`integer`

- minimum value: `1`
- maximum value: `2147483647`

### EnableTransactionLog

Defines whether the Storage component maintains a transaction log between checkpoint operations.  The transaction log helps the product reduce data loss, should the host device lose power.

#### EnableTransactionLog type

`bool`

### TransactionLogLimitMB

Defines the maximum size, in MB, of a transaction log.  Should a transaction log exceed this size, it will be deleted, thus reducing the amount of data that can be recovered should the host device lose power.

#### TransactionLogLimitMB type

`integer`

- minimum value: `1`
- maximum value: `2147483647`

### CheckpointRateInSec

Defines how often the storage component ensures recent data and configuration changes are flushed to storage.  

A setting of 0 disables checkpointing.  Disabling checkpointing reduces the resiliency of the product and thus data loss can occur should the host device lose power.

The value is expressed in seconds.

#### CheckpointRateInSec type

`integer`

- minimum value: `0`
- maximum value: `86400`

**Note:** All of the following _requirements_ need to be fulfilled.

##### Requirement 1

- []() � `#/definitions/EdgeConfigurationBase`

##### Requirement 2

`object` with following properties:

| Property                 | Type    | Required     |
| ------------------------ | ------- | ------------ |
| `IngressDebugExpiration` | string  | **Required** |
| `StreamStorageLimitMb`   | integer | **Required** |
| `StreamStorageTargetMb`  | integer | **Required** |
| `EnableTransactionLog`   | bool    | Optional     |
| `TransactionLogLimitMB`  | integer | Optional     |
| `CheckpointRateInSec`    | integer | Optional     |
