# The Bazel buildtools repo contains tools like the BUILD file formatter, buildifier
# This commit matches the version of buildifier in angular/ngcontainer
# If you change this, also check if it matches the version in the angular/ngcontainer
# version in /.circleci/config.yml
BAZEL_BUILDTOOLS_VERSION = "49a6c199e3fbf5d94534b2771868677d3f9c6de9"

http_archive(
    name = "com_github_bazelbuild_buildtools",
    url = "https://github.com/bazelbuild/buildtools/archive/%s.zip" % BAZEL_BUILDTOOLS_VERSION,
    strip_prefix = "buildtools-%s" % BAZEL_BUILDTOOLS_VERSION,
    sha256 = "edf39af5fc257521e4af4c40829fffe8fba6d0ebff9f4dd69a6f8f1223ae047b",
)

# The @angular repo contains rule for building Angular applications
http_archive(
    name = "angular",
    url = "https://github.com/angular/angular/archive/08e4489cf5a93a352954f1639da5e92112993753.zip",
    strip_prefix = "angular-08e4489cf5a93a352954f1639da5e92112993753",
)

# The @rxjs repo contains targets for building rxjs with bazel
http_archive(
    name = "rxjs",
    url = "https://registry.yarnpkg.com/rxjs/-/rxjs-6.3.3.tgz",
    strip_prefix = "package/src",
    sha256 = "72b0b4e517f43358f554c125e40e39f67688cd2738a8998b4a266981ed32f403",
)

# These local_repository rules are needed to prevent `bazel build ...` from
# drilling down into @rxjs workspace BUILD files under node_modules.
# In the future this will no longer be needed.
# TODO(alexeagle): remove after Bazel 0.18 upgrade
local_repository(
    name = "rxjs_ignore",
    path = "node_modules/rxjs/src",
)
local_repository(
    name = "rxjs_ignore_nested_1",
    path = "node_modules/@angular-devkit/core/node_modules/rxjs/src",
)
local_repository(
    name = "rxjs_ignore_nested_2",
    path = "node_modules/@angular-devkit/schematics/node_modules/rxjs/src",
)
local_repository(
    name = "rxjs_ignore_nested_3",
    path = "node_modules/@angular/cli/node_modules/rxjs/src",
)

####################################
# Load and install our dependencies downloaded above.

load("@angular//packages/bazel:package.bzl", "rules_angular_dependencies")

rules_angular_dependencies()

load("@build_bazel_rules_nodejs//:defs.bzl", "check_bazel_version", "node_repositories", "yarn_install")

# The minimum bazel version to use with this example repo is 0.17.1
check_bazel_version("0.17.1")
node_repositories(
    node_version = "10.9.0",
    yarn_version = "1.9.2",
)

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

load("@io_bazel_rules_go//go:def.bzl", "go_rules_dependencies", "go_register_toolchains")

go_rules_dependencies()
go_register_toolchains()

load("@io_bazel_rules_webtesting//web:repositories.bzl", "browser_repositories", "web_test_repositories")

web_test_repositories()
browser_repositories(
    chromium = True,
    firefox = True,
)

load("@build_bazel_rules_typescript//:defs.bzl", "ts_setup_workspace", "check_rules_typescript_version")

ts_setup_workspace()

load("@io_bazel_rules_sass//sass:sass_repositories.bzl", "sass_repositories")

sass_repositories()

load("@angular//:index.bzl", "ng_setup_workspace")

ng_setup_workspace()
