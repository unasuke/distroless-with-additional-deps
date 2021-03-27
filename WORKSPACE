workspace(name='python-test')
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_file")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

git_repository(
    name = "rules_pkg",
    remote = "https://github.com/bazelbuild/rules_pkg.git",
    tag = "0.4.0"
)

load("@rules_pkg//pkg:deps.bzl", "rules_pkg_dependencies")
rules_pkg_dependencies()

load("@rules_pkg//deb_packages:deb_packages.bzl", "deb_packages")

http_file(
    name = "buster_archive_key",
    sha256 = "9c854992fc6c423efe8622c3c326a66e73268995ecbe8f685129063206a18043",
    urls = ["https://ftp-master.debian.org/keys/archive-key-10.asc"],
)

deb_packages(
  name = "depends_python_gmpy2_debian_buster",
  arch = "amd64",
  distro = "buster",
  distro_type = "debian",
  mirrors = ["https://ftp.debian.org/debian"],
  packages = {
    "libgmp10": "pool/main/g/gmp/libgmp10_6.1.2+dfsg-4_amd64.deb",
    "libmpc3": "pool/main/m/mpclib3/libmpc3_1.1.0-1_amd64.deb",
    "libmpfr6": "pool/main/m/mpfr4/libmpfr6_4.0.2-1_amd64.deb",
  },
  packages_sha256 = {
    "libgmp10": "d9c9661c7d4d686a82c29d183124adacbefff797f1ef5723d509dbaa2e92a87c",
    "libmpc3": "a73b05c10399636a7c7bff266205de05631dc4af502bfb441cbbc6af0a7deb2a",
    "libmpfr6": "d005438229811b09ea9783491c98b145c9bcf6489284ad7870c19d2d09a8f571",
  },
  pgp_key = "buster_archive_key",
)

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "95d39fd84ff4474babaf190450ee034d958202043e366b9fc38f438c9e6c3334",
    strip_prefix = "rules_docker-0.16.0",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.16.0/rules_docker-v0.16.0.tar.gz"],
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)
container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")
container_deps()

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)
container_pull(
  name = "python_distroless",
  registry = "gcr.io",
  repository = "distroless/python3-debian10",
  tag = "latest"
)
