# SyntaxNet/DRAGNN

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

proto_library(
  name = "spec-proto",
  srcs = ["dragnn/protos/spec.proto"],
)

cc_proto_library(
  name = "spec",
  deps = ["spec-proto"],
)

# Until Bazel supports python protocol buffer compilation, this step
# needs to be done manually by running the following command:
# bazel-out/host/bin/external/com_google_protobuf/protoc third_party/syntaxnet/dragnn/protos/spec.proto --python_out=.
#
#py_proto_library(
#  name = "pyspec",
#  deps = ["spec-proto"],
#)

cc_library(
  name = "syntaxnet",
  srcs = [
    "dragnn/core/component_registry.cc",
  ],
  hdrs = [
    "dragnn/core/component_registry.h",
    "dragnn/core/input_batch_cache.h",
    "dragnn/core/interfaces/component.h",
    "dragnn/core/interfaces/input_batch.h",
    "dragnn/core/interfaces/transition_state.h",
  ],
  deps = [
    ":spec",
    "//base",
    "//base:registry",
    "//third_party/tensorflow",
  ],
  includes = ["."],
)

cc_library(
  name = "dragnn-ops",
  srcs = [
    "dragnn/core/compute_session_pool.cc",
    "dragnn/core/compute_session.cc",
    "dragnn/core/index_translator.cc",
    "dragnn/core/ops/compute_session_op.cc",
    "dragnn/core/ops/dragnn_ops.cc",
    "dragnn/core/ops/dragnn_op_kernels.cc",
    "dragnn/core/ops/embedding_ops.cc",
    "dragnn/core/ops/embedding_op_kernels.cc",
  ],
  hdrs = [
    "dragnn/core/compute_session.h",
    "dragnn/core/compute_session_pool.h",
    "dragnn/core/index_translator.h",
    "dragnn/core/resource_container.h",
    "dragnn/core/ops/compute_session_op.h",
  ],
  deps = [
    ":syntaxnet",
    "//base",
    "//third_party/tensorflow",
    "//util:embeddings",
  ],
  alwayslink = 1,
)

