package(default_visibility = ["//visibility:public"])

py_library(
    name = "shared",
    srcs = glob(["shared/*.py"]),
)

py_library(
    name = "simulator",
    srcs = glob(["simulator_control/*.py"]),
    deps = [
        ":shared",
    ],
)

py_binary(
    name = "ios_test_runner",
    srcs = ["__init__.py"] + glob(
        ["test_runner/*.py"],
        exclude = ["test_runner/TestProject/**"],
    ),
    compiler_args = [
        "--interpreter",
        "/usr/bin/python3",
    ],
    data = glob(["test_runner/TestProject/**"]),
    main = "test_runner/ios_test_runner.py",
    python_version = "PY3",
    deps = [
        ":shared",
        ":simulator",
    ],
)

# Consumed by bazel tests.
filegroup(
    name = "for_bazel_tests",
    testonly = 1,
    srcs = glob(["**/*"]),
    # Exposed publicly just so other rules can use this if they set up
    # integration tests that need to copy all the support files into
    # a temporary workspace for the tests.
    visibility = ["//visibility:public"],
)
