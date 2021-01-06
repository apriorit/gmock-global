load("@rules_cc//cc:defs.bzl", "cc_library", "cc_test")

package(default_visibility = ["//visibility:public"])

cc_library(
    name = "gmock-global",
    srcs = glob(
        ["*/**/*.cpp"],
    ),
    hdrs = glob(["*/**/*.h"]),
    includes = [
        "include",
    ],
    strip_include_prefix = "include",
)