# PRAXO-CORE D Core

PRAXO-CORE is an embeddable, MIT-licensed agent framework. This package is its
native D Core: an agent loop with tool registration and dispatch, policy hooks,
typed events, memory, checkpoints, context budgets, middleware, JSON Schema
validation, and plugin manifest parsing.

This repository is the D publication split of
[`axisvela/praxo-core`](https://github.com/axisvela/praxo-core). The source of
truth, conformance vectors, and test runners remain in the main repository.

- `SPEC_VERSION`: `0.2.0`
- Core version: `0.1.0`
- Tier: core
- License: MIT
- Dependencies: D standard library only

## Scope

The Core implements all eleven vector groups: toolcall, JSON Schema, plugin,
memory, event, stream, checkpoint, policy, context, middleware, and the agent
loop. It includes a public API snapshot.

## Validation

This split repository contains the DUB package only. Conformance and tests run
in the [main repository](https://github.com/axisvela/praxo-core/tree/main/language/d):

```bash
dmd -i -Isource -O -release source/conformance.d -of=build/conformance
./build/conformance
dmd -i -Isource -O -release source/tests.d -of=build/tests
./build/tests
```

## Quickstart

```d
import praxo.agent;
import praxo.models;

void main() {
    auto options = new AgentOptions(new StaticModel("hello"));
    auto result = runAgent(options, Session("demo"), "hello");
    writeln(result.output);
}
```

Tools register on the options object:

```d
auto registry = new Registry();
registry.register(new FuncTool("echo", "Echo arguments", (arguments) => arguments));
options.tools = registry;
```

## Layout

- `source/praxo/` package modules.
- `api/0.1.0.txt` public API snapshot.

## Release

Tag shape: `v0.1.0`. The main source repository uses `d/v0.1.0`; this split
repository is what code.dlang.org registers.
