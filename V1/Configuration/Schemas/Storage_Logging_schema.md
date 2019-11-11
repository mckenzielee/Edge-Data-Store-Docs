---
uid: Storage_Logging_schema
---

# Storage logging configuration schema

The Storage logging configuration schema specifies how to formally describe the logging parameters for Storage.

| Abstract            | Extensible | Status       | Identifiable | Custom properties | Additional properties |
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- |
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             |

# StorageLoggerConfiguration Properties

| Property                                        | Type      | Required | Nullable | Defined by                            |
| ----------------------------------------------- | --------- | -------- | -------- | ------------------------------------- |
| [LogFileCountLimit](#logfilecountlimit)         | `integer` | Optional | Yes      | EdgeLoggerConfiguration (this schema) |
| [LogFileSizeLimitBytes](#logfilesizelimitbytes) | `integer` | Optional | Yes      | EdgeLoggerConfiguration (this schema) |
| [LogLevel](#loglevel)                           | reference | Optional | No       | EdgeLoggerConfiguration (this schema) |


**Note:** All of the following _requirements_ need to be fulfilled.

#### Requirement 1

- []() – `#/definitions/EdgeConfigurationBase`

#### Requirement 2

`object` with following properties:

| Property                | Type    | Required |
| ----------------------- | ------- | -------- |
| `LogFileCountLimit`     | integer | Optional |
| `LogFileSizeLimitBytes` | integer | Optional |
| `LogLevel`              |         | Optional |
