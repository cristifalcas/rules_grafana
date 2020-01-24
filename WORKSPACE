workspace(name = "io_bazel_rules_grafana")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# rules go
bazel_rules_go_version = "v0.20.2"

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "b9aa86ec08a292b97ec4591cf578e020b35f98e12173bbd4a921f84f583aebd9",
    url = "https://github.com/bazelbuild/rules_go/releases/download/%s/rules_go-%s.tar.gz" % (bazel_rules_go_version, bazel_rules_go_version),
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains()

# rules gazelle
http_archive(
    name = "bazel_gazelle",
    sha256 = "86c6d481b3f7aedc1d60c1c211c6f76da282ae197c3b3160f54bd3a8f847896f",
    urls = ["https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.19.1/bazel-gazelle-v0.19.1.tar.gz"],
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

rules_python_version = "3d3725f4d77527c3b1a6b0a318b274876ae09a4f"

http_archive(
    name = "rules_python",
    sha256 = "b87a58c84ee32e26754fb455c47b1c523c30177211e933fb6249eea06cf1c14d",
    strip_prefix = "rules_python-%s" % rules_python_version,
    type = "zip",
    urls = [
        "https://github.etsycorp.com/Engineering/rules_python/archive/%s.zip" % rules_python_version,
    ],
)

load("@rules_python//python:pip.bzl", "pip_repositories")

pip_repositories()

rules_docker_version = "0.14.1"

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "cc6144e61d87b96f219bc5392ecf92fef01ca30da502ed543b4524625bdf06a2",
    strip_prefix = "rules_docker-%s" % rules_docker_version,
    urls = ["https://github.com/bazelbuild/rules_docker/archive/v%s.zip" % rules_docker_version],
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

load(
    "@io_bazel_rules_docker//repositories:go_repositories.bzl",
    container_go_deps = "go_deps",
)

container_go_deps()

# end external rules

load("@io_bazel_rules_grafana//grafana:workspace.bzl", "grafana_plugin", "repositories")

repositories()

load("@io_bazel_rules_grafana_deps3//:requirements.bzl", pip_install3 = "pip_install")

pip_install3()

grafana_plugin(
    name = "grafana_plotly_plugin",
    sha256 = "ba67afef48c9ce6c96978dd8d7e2ff2dc1f09e6cfd7eccf89bfaaf574347cd52",
    type = "zip",
    urls = ["https://grafana.com/api/plugins/natel-plotly-panel/versions/0.0.5/download"],
)
