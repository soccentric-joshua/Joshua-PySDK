# Joshua-PySDK Build and Deployment

## Purpose and scope

Joshua-PySDK is the Python SDK for the Joshua HAL service. The `joshua-sdk` package targets Python 3.10+, depends on `grpcio` and protobuf, and includes generated protobuf/dataclass bindings. The root Makefile uses `uv` to create the environment, install the package in editable mode, regenerate/check bindings, run tests, lint, type-check, and build distributions.

## 1. Prerequisites

- Python 3.10 or newer.
- `uv` on PATH, or pass `UV=/path/to/uv`.
- Network/package access for `uv` to resolve dependencies. The SDK development extra installs grpc tooling, pytest/coverage, mypy, ruff, PyYAML, and typing packages.
- The proto generation tools and expected Joshua-HAL proto inputs must be available to `tools/gen_proto.py`; generation is not a runtime hardware test.

## 2. Setup

Run `make setup` to create `.venv` with `uv` and install `joshua-sdk[dev]` from `joshua-sdk/` in editable mode. `make venv` creates only the environment. Override `VENV` or `UV` when integrating with another local toolchain.

## 3. Build and compile

- `make gen` - regenerate protobuf and dataclass bindings.
- `make gen-check` - regenerate into a temporary comparison flow and fail when committed stubs are stale.
- `make gen-clean` - remove generated proto output and perform a full regeneration.
- `make build` - install the `build` helper into the uv environment and create wheel plus sdist under `joshua-sdk/dist`.
- `make shell` - enter a uv-activated subshell.

Generated output is `joshua-sdk/src/joshua_sdk/_proto`. Treat generated changes as source-controlled artifacts and review them after `make gen`.

## 4. Test and lint

- `make test` - run pytest with coverage and terminal-missing reporting.
- `make lint` - run Ruff on the SDK source.
- `make typecheck` - run strict mypy using `joshua-sdk/pyproject.toml`.
- `make check` - run lint, typecheck, and test.
- `make` or `make all` - the default aggregate check.

The package configuration excludes generated proto/type directories from normal Ruff and strict mypy analysis. Tests are local Python tests and do not by themselves verify a live HAL endpoint.

## 5. Packaging and artifacts

`make build` produces the Python wheel and source distribution in `joshua-sdk/dist`. Editable installation uses the virtual environment and does not create a deployment image. The generated binding tree is a separate source artifact managed by `make gen`.

## 6. Deployment, install, and run

There is no deployment or service-run target in this Makefile. Install the built wheel into a target environment with its Python 3.10+ runtime and compatible `grpcio`/protobuf versions, then use the SDK's documented client API to connect to a reachable HAL gRPC service. Endpoint credentials, network addresses, and target service lifecycle are external to this repository.

## 7. Cleanup

- `make clean` removes package build/dist/egg-info, pytest/mypy/ruff caches, coverage output, and Python bytecode while keeping `.venv`.
- `make distclean` also removes `.venv` and stamp files.
- `make gen-clean` removes generated stubs before regenerating them.

## 8. Hardware, cloud, and manual verification caveats

No cloud deployment is automated. Unit tests, lint, type-check, and wheel creation can run without hardware. Manual verification must install the artifact in a controlled target environment and exercise a real compatible HAL gRPC endpoint, including protobuf compatibility, network access, authentication if provided by the service, and device-specific behavior.
