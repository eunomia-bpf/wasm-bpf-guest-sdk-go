# wasm-bpf-guest-sdk-go
Guest SDK of wasm-bpf, for Go programs

It provides a go file with wasm-bpf API bindings. Can be used in tinygo for WASI targets.

## File-descriptor attach

`WasmAttachBpfProgramFd(object, programName, targetFd)` attaches a program from
the object handle returned by `WasmLoadBpfObject`. `programName` is a pointer to
the NUL-terminated program name in guest memory, and `targetFd` is a guest file
descriptor for a directory preopened by the runtime. The function returns `0`
on success and a runtime-specific negative value on failure.

TinyGo omits this host import when a guest does not call the function, so merely
rebuilding an existing guest with this SDK does not raise its minimum wasm-bpf
runtime version. Guests that call it require a runtime providing
`wasm_bpf.wasm_attach_bpf_program_fd`.
