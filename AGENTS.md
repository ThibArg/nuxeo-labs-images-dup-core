# Project Guidelines

## Project and Runtime

- This is a Maven multi-module Nuxeo LTS 2025 plugin. The root POM builds the `nuxeo-labs-images-dup-core` bundle and `nuxeo-labs-images-dup-package`.
- Keep the plugin version at `2025.1.0` and the Java runtime/target at Java 21 to match the supported Nuxeo LTS environment.
- The core bundle computes perceptual hashes, stores band keys on Picture documents, searches through NXQL with the caller's principal, and exposes listener, bulk-action, service, and Automation-operation integrations.

## Java Conventions

- Follow the Java conventions in the Nuxeo LTS 2025 source tree's `AGENTS.md`; when instructions conflict, that file takes precedence.
- Use Java 21 features where they improve clarity, including `var` for obvious local types, records for immutable value types, pattern matching, switch expressions, text blocks, and `String.formatted()`.
- Use 4-space indentation, K&R braces, no wildcard imports, and keep lines near 120 characters.
- Use Log4j2 with parameterized messages. Do not write to standard output or use SLF4J directly.
- Add `@since 2025.1.0` to public API introduced by this plugin. Keep Apache 2.0 license headers on Java files.
- Use Nuxeo APIs for repository access and permission-aware searches. Do not bypass `CoreSession` authorization.
- Use try-with-resources for closeable resources. Handle specific exceptions; do not catch `Exception`, `Throwable`, or `Error` broadly.
- Temporary files must use Nuxeo's managed temporary directory or `Framework` temporary-file helpers. Configure ImageIO caching to use Nuxeo's temporary directory.

## Build and Test

- Run `mvn clean install` from the repository root for the full reactor build and tests.
- Tests are JUnit 4 tests under `nuxeo-labs-images-dup-core/src/test/java`.
- Apply the project's configured Spotless formatting when the workspace is a Git checkout; Spotless requires Git metadata.
