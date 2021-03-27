load("@depends_python_gmpy2_debian_buster//debs:deb_packages.bzl", "depends_python_gmpy2_debian_buster")
load("@io_bazel_rules_docker//container:container.bzl", "container_image")

container_image(
  name ="python_with_gmpy2_depends",
  base="@python_distroless//image",
  debs=[
    depends_python_gmpy2_debian_buster["libgmp10"],
    depends_python_gmpy2_debian_buster["libmpc3"],
    depends_python_gmpy2_debian_buster["libmpfr6"],
  ],
)
