#
# Copyright (C) 2020 Grakn Labs
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU Affero General Public License as
# published by the Free Software Foundation, either version 3 of the
# License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU Affero General Public License for more details.
#
# You should have received a copy of the GNU Affero General Public License
# along with this program.  If not, see <https://www.gnu.org/licenses/>.
#

package(default_visibility = ["//visibility:public"])
load("@stackb_rules_proto//java:java_grpc_compile.bzl", "java_grpc_compile")
load("@graknlabs_build_tools//distribution/maven:rules.bzl", "assemble_maven", "deploy_maven")

java_grpc_compile(
    name = "protocol-src",
    deps = [
        "//keyspace:keyspace-proto",
        "//session:session-proto",
        "//session:answer-proto",
        "//session:concept-proto",
    ]
)

java_library(
    name = "protocol",
    srcs = [":protocol-src"],
    deps = [
        "//dependencies/maven/artifacts/com/google/guava:guava",
        "//dependencies/maven/artifacts/com/google/protobuf:protobuf-java",
        "//dependencies/maven/artifacts/io/grpc:grpc-core",
        "//dependencies/maven/artifacts/io/grpc:grpc-protobuf",
        "//dependencies/maven/artifacts/io/grpc:grpc-stub",
        "//dependencies/maven/artifacts/io/grpc:grpc-api",
    ],
    tags = ["maven_coordinates=io.grakn.protocol:grakn-protocol:{pom_version}", "checkstyle_ignore"],
)

assemble_maven(
    name = "assemble-maven",
    target = ":protocol",
    package = "grpc",
    workspace_refs = "@graknlabs_protocol_workspace_refs//:refs.json"
)

deploy_maven(
    name = "deploy-maven",
    target = ":assemble-maven"
)

# --- KGMS console dependencies

java_grpc_compile(
    name = "kgms-console-protocol-src",
    deps = ["//kgms:console-proto"]
)

java_library(
    name = "kgms-console-protocol-java",
    srcs = [":kgms-console-protocol-src"],
    deps = [
        "//dependencies/maven/artifacts/com/google/protobuf:protobuf-java",
        "//dependencies/maven/artifacts/io/grpc:grpc-core",
        "//dependencies/maven/artifacts/io/grpc:grpc-protobuf",
        "//dependencies/maven/artifacts/io/grpc:grpc-stub",
        "//dependencies/maven/artifacts/io/grpc:grpc-api",
    ],
    visibility = ["//visibility:public"],
    tags = ["checkstyle_ignore"]
)

