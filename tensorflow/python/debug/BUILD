# Description:
#   Python Client Code of the TensorFlow Debugger (tfdbg).

package(
    default_visibility = ["//tensorflow:internal"],
    features = [
        "-layering_check",
        "-parse_headers",
    ],
)

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

load("//tensorflow:tensorflow.bzl", "cuda_py_test")

py_library(
    name = "debug_data",
    srcs = ["debug_data.py"],
    srcs_version = "PY2AND3",
)

py_library(
    name = "debug_utils",
    srcs = ["debug_utils.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/python:session",
    ],
)

py_library(
    name = "framework",
    srcs = ["framework.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":debug_utils",
        "//tensorflow/python:session",
    ],
)

py_library(
    name = "debugger_cli_common",
    srcs = ["cli/debugger_cli_common.py"],
    srcs_version = "PY2AND3",
)

py_library(
    name = "tensor_format",
    srcs = ["cli/tensor_format.py"],
    srcs_version = "PY2AND3",
    deps = [":debugger_cli_common"],
)

py_library(
    name = "analyzer_cli",
    srcs = ["cli/analyzer_cli.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":debug_data",
        ":debugger_cli_common",
        ":tensor_format",
    ],
)

py_library(
    name = "curses_ui",
    srcs = ["cli/curses_ui.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":debugger_cli_common",
        "//tensorflow:tensorflow_py",
    ],
)

py_library(
    name = "local_cli",
    srcs = ["local_cli.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":analyzer_cli",
        ":curses_ui",
        ":debug_data",
        ":debugger_cli_common",
        ":framework",
        "//tensorflow:tensorflow_py",  # TODO(cais): Change in buildozer.yml.
        "//tensorflow/python:session",
    ],
)

py_binary(
    name = "debug_fibonacci",
    srcs = ["examples/debug_fibonacci.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":local_cli",
        "//tensorflow:tensorflow_py",
    ],
)

py_binary(
    name = "debug_mnist",
    srcs = ["examples/debug_mnist.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":debug_data",
        ":local_cli",
        "//tensorflow:tensorflow_py",
        "//tensorflow/examples/tutorials/mnist:input_data",
    ],
)

py_test(
    name = "debug_data_test",
    size = "small",
    srcs = [
        "debug_data_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":debug_data",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_test_lib",
    ],
)

py_test(
    name = "debug_utils_test",
    size = "small",
    srcs = [
        "debug_utils_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":debug_utils",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:session",
        "//tensorflow/python:variables",
    ],
)

py_test(
    name = "framework_test",
    size = "small",
    srcs = [
        "framework_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":debug_data",
        ":framework",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:session",
        "//tensorflow/python:variables",
    ],
)

py_test(
    name = "curses_ui_test",
    size = "small",
    srcs = [
        "cli/curses_ui_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":curses_ui",
        ":debugger_cli_common",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_test_lib",
    ],
)

cuda_py_test(
    name = "session_debug_test",
    size = "small",
    srcs = [
        "session_debug_test.py",
    ],
    additional_deps = [
        ":debug_data",
        ":debug_utils",
        "//tensorflow:tensorflow_py",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:session",
    ],
)

py_test(
    name = "debugger_cli_common_test",
    size = "small",
    srcs = [
        "cli/debugger_cli_common_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":debugger_cli_common",
        "//tensorflow/python:framework_test_lib",
    ],
)

py_test(
    name = "tensor_format_test",
    size = "small",
    srcs = [
        "cli/tensor_format_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":tensor_format",
        "//tensorflow/python:framework_test_lib",
    ],
)

cuda_py_test(
    name = "analyzer_cli_test",
    size = "small",
    srcs = [
        "cli/analyzer_cli_test.py",
    ],
    additional_deps = [
        ":analyzer_cli",
        ":debug_data",
        ":debug_utils",
        ":debugger_cli_common",
        "//tensorflow:tensorflow_py",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:session",
    ],
)

py_test(
    name = "local_cli_test",
    size = "small",
    srcs = [
        "local_cli_test.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":local_cli",
        "//tensorflow:tensorflow_py",  # TODO(cais): Buildozer rule.
        "//tensorflow/python:framework_test_lib",
    ],
)

filegroup(
    name = "all_files",
    srcs = glob(
        ["**/*"],
        exclude = [
            "**/METADATA",
            "**/OWNERS",
        ],
    ),
    visibility = ["//tensorflow:__subpackages__"],
)
