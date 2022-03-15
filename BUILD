load("@rules_rust//bindgen:bindgen.bzl", "rust_bindgen")

cc_library(
    name = "example_lib",
    hdrs = ["example.h"]
)

rust_bindgen(
    name = "example_bindings",
    cc_lib = ":example_lib",
    header = "example.h",
    bindgen_flags = [
        "--allowlist-function=max_uint32_t",
    ],
)

platform(
    name = "linux_x86_64",
    constraint_values = [
        "@platforms//os:linux",
        "@platforms//cpu:x86_64",
    ],
    exec_properties = {
        "os": "linux",
        "cpu": "x86_64",
        "env-vars": """{"WORKER_ASSIGNED_CPUS": "{{limits.cpu.claimed}}"}""",
    },
)
