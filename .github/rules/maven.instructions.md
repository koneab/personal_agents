---
description: Maven build and pom.xml rules for Spring Boot projects.
applyTo: '**/pom.xml'
---

## Parent and dependencies
- Inherit from `spring-boot-starter-parent` or import `spring-boot-dependencies` in `dependencyManagement`; let Boot manage dependency versions.
- Do not declare versions for dependencies already managed by the Boot BOM.
- Centralise any other version in `<properties>`; never repeat a literal version.
- Use the narrowest starter (`spring-boot-starter-web`, `-data-jpa`, `-validation`, `-security`, `-test`); no unused dependencies.
- Set `<scope>test</scope>` for test-only libraries and `<scope>runtime</scope>` for drivers.
- Do not use version ranges, `LATEST`, `RELEASE` or `SNAPSHOT` dependencies in release builds.

## Build configuration
- Declare the Java version once (`<java.version>`) and keep it consistent with the toolchain and CI.
- Set `project.build.sourceEncoding` and `project.build.outputTimestamp` for reproducible builds.
- Pin plugin versions; do not rely on Maven's default plugin versions.
- Use `spring-boot-maven-plugin` for packaging; keep plugin configuration minimal.
- Run Checkstyle and SpotBugs from the build with the project's checked-in configuration; do not weaken rules to pass the build.
- Keep unit tests in Surefire (`*Test`) and integration tests in Failsafe (`*IT`).

## Modules and hygiene
- In multi-module builds, keep the parent as an aggregator with `dependencyManagement`; modules declare only the dependencies they use.
- Run Maven in batch mode (`-B`) in automation.
- Never put credentials or tokens in `pom.xml` or `settings.xml` committed to the repository.
- Run dependency vulnerability checks (OWASP Dependency-Check or equivalent) in CI when the project configures them.
