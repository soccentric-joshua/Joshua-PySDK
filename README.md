# Joshua-PySDK

## Project Summary

Joshua-PySDK is the Python client library for invoking Joshua-HAL through the `HalService` endpoint exposed by Joshua-Client. The distributable package is `joshua-sdk` and the primary import is `joshua_sdk`; the repository also keeps an `acadia_sdk` deprecation shim for callers using the previous package name. The package under `joshua-sdk/` includes typed client, channel, conversion, exception, peripheral, and generated protobuf modules.

The public workflow is a Pythonic gRPC client that can discover a target, connect to HalService, invoke one-shot tests, start long-running tests, monitor events, and represent results through the SDK’s typed surface. Examples include a long-running test and a self-test-all flow. Documentation covers quick start, API reference, peripherals, error handling, versioning, release notes, and generated-code expectations. The test suite uses fake server fixtures and covers connection, discovery, event handling, deprecation compatibility, long-running calls, monitoring, one-shot calls, and type round trips. Those tests establish client-side coverage, but a real Joshua-Client, generated-protobuf compatibility, hardware result, and network failure scenario still need manual integration runs. The Makefile documents setup, generation, checks, and package build operations.

## Feature Inventory

| # | Name / Description | Implemented? | Test Coverage? | Manual Test |
|---:|---|---|---|---|
| 1 | `joshua-sdk` distributable package | Implemented | Package tests | [ ] Manual verification required |
| 2 | `joshua_sdk` public import | Implemented | Import/client tests | [ ] Manual verification required |
| 3 | `acadia_sdk` deprecation shim | Implemented | `test_deprecation_shim.py` | [ ] Manual verification required |
| 4 | gRPC channel and client connection | Implemented | `test_connect.py` | [ ] Manual verification required |
| 5 | Device discovery | Implemented | `test_discovery.py` | [ ] Manual verification required |
| 6 | One-shot execution | Implemented | `test_oneshot.py` | [ ] Manual verification required |
| 7 | Long-running execution | Implemented | `test_long_running.py` | [ ] Manual verification required |
| 8 | Monitoring and events | Implemented | `test_monitor.py`, `test_event.py` | [ ] Manual verification required |
| 9 | Typed protobuf/result round trips | Implemented | `test_types_roundtrip.py` | [ ] Manual verification required |
| 10 | Peripheral and generated protobuf modules | Implemented | Partial indirect coverage | [ ] Manual verification required |
| 11 | Fake server fixtures | Implemented | Used by package tests | [ ] Manual verification required |
| 12 | Examples and API documentation | Implemented | Examples not automated tests | [ ] Manual verification required |
| 13 | Setup/generation/check/build targets | Implemented | Unknown | [ ] Manual verification required |
| 14 | Live Joshua-Client/HAL compatibility | Partial | Not covered by fake server | [ ] Manual verification required |

## Test and Build References

```bash
cd joshua-sdk
make setup && make gen && make check && make build
pytest tests
```# Joshua-PySDK

## Project Summary

Joshua-PySDK is the Python client library for invoking Joshua-HAL through the
`HalService` endpoint exposed by Joshua-Client. The distributable package is
`joshua-sdk` and the primary import is `joshua_sdk`; the repository also keeps
an `acadia_sdk` deprecation shim for callers using the previous package name.
The actual SDK package lives under `joshua-sdk/` and includes typed client,
channel, conversion, exception, peripheral, and generated protobuf modules.

The public workflow is a Pythonic gRPC client that can discover a target,
connect to a HalService endpoint, invoke one-shot tests, start long-running
tests, monitor events, and represent results through the SDK’s typed surface.
Examples include a long-running test and a self-test-all flow. The package
documentation covers quick start, API reference, peripherals, error handling,
versioning, release notes, and generated-code expectations. The test suite uses
fake server fixtures and covers connection, discovery, event handling,
deprecation compatibility, long-running calls, monitoring, one-shot calls, and
type round trips. Those tests establish meaningful client-side coverage, but a
real Joshua-Client, generated-protobuf compatibility, hardware result, and
network failure scenario still need manual integration runs. The Makefile
documents setup, protobuf generation, checks, and package build operations.
This README keeps the useful package pointers from the previous leaf README
while separating implemented client behavior from planned or environment-bound
integration claims.

## Feature Inventory

| # | Name / Description | Implemented? | Test Coverage? | Manual Test |
|---:|---|---|---|---|
| 1 | `joshua-sdk` distributable package | Implemented | Covered by package tests | [ ] Manual verification required |
| 2 | `joshua_sdk` public import surface | Implemented | Covered by import/client tests | [ ] Manual verification required |
| 3 | `acadia_sdk` deprecation shim | Implemented | Covered by `test_deprecation_shim.py` | [ ] Manual verification required |
| 4 | gRPC channel and client connection | Implemented | Covered by `test_connect.py` | [ ] Manual verification required |
| 5 | Device discovery | Implemented | Covered by `test_discovery.py` | [ ] Manual verification required |
| 6 | One-shot test execution | Implemented | Covered by `test_oneshot.py` | [ ] Manual verification required |
| 7 | Long-running test execution | Implemented | Covered by `test_long_running.py` | [ ] Manual verification required |
| 8 | Monitoring and event handling | Implemented | Covered by `test_monitor.py` and `test_event.py` | [ ] Manual verification required |
| 9 | Typed protobuf/result round trips | Implemented | Covered by `test_types_roundtrip.py` | [ ] Manual verification required |
| 10 | Peripheral and generated protobuf modules | Implemented | Partial; generated surface is indirectly covered | [ ] Manual verification required |
| 11 | Fake server test fixtures | Implemented | Used by the package test suite | [ ] Manual verification required |
| 12 | User examples and API documentation | Implemented | Examples are not automated tests | [ ] Manual verification required |
| 13 | Setup, generation, check, and build Make targets | Implemented | Unknown | [ ] Manual verification required |
| 14 | Compatibility with a live Joshua-Client/HAL target | Partial | Not covered by fake-server tests | [ ] Manual verification required |

## Test and Build References

```bash
cd joshua-sdk
make setup
make gen
make check
make build
pytest tests
```

See `joshua-sdk/README.md`, `docs/api_reference.md`, and `docs/quickstart.md`.
SiliconCentric `project-managers` fleet. This leaf provides `joshua-sdk`, a Pythonic gRPC client for the `HalService`
endpoint exposed by `Joshua-Client`. The SDK distribution package is
**`joshua-sdk`** (import name `joshua_sdk`); a `acadia_sdk` deprecation shim
re-exports the public surface for callers still on the old name. The SDK source, tooling, docs, examples, and test suite live under
[`joshua-sdk/`](joshua-sdk). See [`joshua-sdk/README.md`](joshua-sdk/README.md)
for the full API, quickstart, and `make` targets (`setup`, `gen`, `check`,
`build`). ---
Part of the `Joshua` project in the `project-managers` fleet. See
`docs/project-managers.md` for the full 9-project/ 8-leaf hierarchy and
shared conventions.