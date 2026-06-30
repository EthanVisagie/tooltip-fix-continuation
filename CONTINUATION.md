# Tooltip Fix Continuation

This fork starts from `hetpatel-11/Adobe_Premiere_Pro_MCP` commit `8bde85362311ddbb7ff28eda50e342013fe67511`.

## Local Setup State

- Built and smoke-tested on Windows with Node 22.
- Registered locally with Codex as `premiere_pro`.
- Installed CEP bridge into `%APPDATA%\Adobe\CEP\extensions\com.mcp.premiere.cepbridge`.
- Used shared bridge temp directory `%TEMP%\premiere-mcp-bridge`.

## Local Changes

- Upgraded runtime dependencies to remove known npm audit issues:
  - `@modelcontextprotocol/sdk` to `^1.29.0`
  - `uuid` to `^11.1.1`
  - `ws` resolved to `8.21.0`
- Added the local Windows Premiere install path:
  - `D:\Adobe\Adobe Premiere Pro 2024\Adobe Premiere Pro.exe`

## Verification

- `npm run build` passes.
- `npm audit --omit=dev` reports zero vulnerabilities.
- MCP stdio smoke test initializes successfully and lists 278 tools.

## Known Gaps

- Full Jest suite is not Windows-clean yet:
  - 108 tests passed.
  - 7 tests failed.
  - Failures are Windows path expectation mismatches and two mock workflow timeouts.
- Live Premiere end-to-end testing still requires opening Premiere, starting the MCP Bridge CEP panel, and running a scratch-project workflow.

## Next Porting Work

- Normalize Windows/macOS path handling in tests.
- Review high-level workflow mock tests that exceed the 10 second Jest timeout.
- Avoid hard-coded local install paths by detecting Premiere from Start Menu entries, registry keys, or configurable environment variables.
- Validate the upgraded MCP SDK against real Codex tool calls in a scratch Premiere project.
