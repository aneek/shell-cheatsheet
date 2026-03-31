# AGENTS.md

This file provides guidance to AI Agents when working with code in this repository.

---

## Reference Documents

The following documents provide guidance to AI Agents when working with code in
this repository and the AI must strictly adhere to them.

- Documentation Guidelines: @docs/GoDocs.md

---

## Project Overview

**shell-cheatsheet** is a project that is just build on top of [gocui](https://github.com/jroimartin/gocui) and provides a overlay window on the current
terminal to show all the available aliases with a filter and execute them if
selected and enter is pressed.

- **Package:** `github.com/aneek/shell-cheatsheet`
- **Min Go version:** 1.22+
- **License:** MIT
- **TUI framework:** gocui

---

## Behavior Guidance

### File Search
- Use search and targeted file reads, do not read every file.
- Prefer `rg` searches to find entry points and configs. If `rg` is not available, then mention this to the user to install it.

### Answering Questions
- When asked a question, consider the answer and perform any exploration of the codebase required to provide a quality answer.
- When asked a question, do not write or modify code. Simply answer the question.

### Communication
- Be direct and straight forward.
- **DO NOT** be overly dramatic or jump to conclusions. 
  e.g. don't say "Critical Memory Safety Issue Found" unless you are certain 
  that is true. 
  If you are not certain, then frame it "Potential Memory Issue Found".
- **DO NOT** be sycophantic or use unnecessary flattery. Avoid phrases like 
  "You're absolutely right".

---


## Development Guidelines

### Build and Development Commands

```bash
# Initialize (first time)
go mod init github.com/bayer-int/wsf-nxg-cli-sdk
go mod tidy

# Build
go build ./...

# Test
go test ./...                              # all tests
go test -race ./...                        # with race detector (always use)
go test -v ./... -run TestFunctionName     # single test
go test -coverprofile=coverage.out ./...   # with coverage
go tool cover -html=coverage.out           # view coverage in browser

# Format
gofmt -w .
goimports -w .
```

### Key Constraints

- Always check the Effective Go documentation - https://go.dev/doc/effective_go
  and understand each sections before writing code to have a better coding style.

### Code style

- **Go 1.22+** minimum. Use modern language features.
- Run `gofmt` / `goimports` on all code. Run `go vet ./...` before committing.
- All exported functions, types, and packages must have doc comments.


### Error handling

- Always return errors — never `os.Exit()` outside `main.go`, never `panic` for control flow.
- Wrap errors with context: `fmt.Errorf("operation %s: %w", key, err)`.
- Use typed errors from `errors/` package (`APIError`, `AuthError`, `ValidationError`).
- All Cobra commands must use `RunE`, not `Run`.

### Output

- **Never** use `fmt.Print*` in non-test code. All output goes through `rt.Output` (the `OutputWriter` interface).
- **Never** use `http.DefaultClient` or construct raw `http.Client{}`. Use `rt.HTTPClient`.
- The custom linter (`wsf-lint`) enforces these rules statically.

### Testing

- Table-driven tests with subtests (`t.Run`).
- Always run with `-race` flag.
- Use `runtime.NewTestRuntime()` for plugin/command tests.
- Target 80%+ coverage for general code, 100% for critical business logic.
- Use `t.Helper()` in helper functions, `t.Cleanup()` for teardown.

### Dependencies

- External dependencies:
  - gocui

---

## Local Norms

---


## Self-Correction

Use the `agents-md-improver` skill for structured updates based on the below
rules.

1. **Stale build and development commands:** If you discover that the Build and 
Development Commands above does not match the actual commands, update this 
`AGENTS.md` file immediately to reflect the current state.

2. **Stale external dependencies:** If you discover that the External Dependencies 
above does not match the actual dependencies, update this `AGENTS.md` file 
immediately to reflect the current state.

3. **User corrections:** If the user gives a correction about how work should be 
done in this repo (naming, process, tooling, patterns), add it to the **Local Norms** section so that future sessions inherit it.

---
