load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_rust",
    sha256 = "8a2052e8ec707aa04a6b9e72bfc67fea44e915ecab1d2d0a4835ad51c2410c36",
    strip_prefix = "rules_rust-b16c26ba5faf1c58ebe94582afd20567ce676e6d",
    urls = [
        "https://github.com/bazelbuild/rules_rust/archive/b16c26ba5faf1c58ebe94582afd20567ce676e6d.tar.gz",
    ],
)

load("@rules_rust//bindgen:repositories.bzl", "rust_bindgen_repositories")
load("@rules_rust//rust:repositories.bzl", "rust_repositories")

rust_repositories(
    edition = "2021",
    include_rustc_srcs = True,
    iso_date = "2022-02-23",
    rustfmt_version = "nightly",
    version = "nightly",
)

rust_bindgen_repositories()
