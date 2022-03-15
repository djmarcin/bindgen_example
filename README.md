# bindgen_example

Demonstration of how rust_bindgen fails under remote execution.

I am using a bazel-buildfarm cluster for execution.

A log of the failure is here:
```
$ bazel build --config=remote :example_bindings
INFO: Invocation ID: 58fc0eb6-43bb-4177-8101-decfcf0f8a5d
INFO: Analyzed target //:example_bindings (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
ERROR: /home/david/bindgen_example/BUILD:8:13: Generating bindings for example.h.. failed: (Exit 1): cargo_bin_bindgen failed: error executing command bazel-out/k8-opt-exec-2F36172C/bin/external/rules_rust_bindgen__bindgen__0_58_1/cargo_bin_bindgen --no-rustfmt-bindings '--allowlist-function=max_uint32_t' example.h --output ... (remaining 6 arguments skipped)
/usr/include/stdio.h:33:10: fatal error: 'stddef.h' file not found
/usr/include/stdio.h:33:10: fatal error: 'stddef.h' file not found, err: true
thread 'main' panicked at 'Unable to generate bindings: ()', external/rules_rust_bindgen__bindgen__0_58_1/src/main.rs:54:36
stack backtrace:
   0: rust_begin_unwind
             at /rustc/68369a041cea809a87e5bd80701da90e0e0a4799/library/std/src/panicking.rs:584:5
   1: core::panicking::panic_fmt
             at /rustc/68369a041cea809a87e5bd80701da90e0e0a4799/library/core/src/panicking.rs:142:14
   2: core::result::unwrap_failed
             at /rustc/68369a041cea809a87e5bd80701da90e0e0a4799/library/core/src/result.rs:1749:5
   3: std::panicking::try
   4: cargo_bin_bindgen::main
note: Some details are omitted, run with `RUST_BACKTRACE=full` for a verbose backtrace.
Target //:example_bindings failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 1.475s, Critical Path: 1.17s
INFO: 2 processes: 2 internal.
FAILED: Build did NOT complete successfully
```

The cause is that libclang.so cannot find the include headers on the remote machine because they are not part of the dependency graph created by the bindgen toolchain.