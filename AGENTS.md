# Repository Instructions

- This repository is a release workflow wrapper, not the Dyomi Android source tree. The workflow checks out `pazbryant7/Dyomi` at build time; do not expect `app/`, `gradlew`, or local tests here.
- The only build workflow is `.github/workflows/BuildPreview.yml`, triggered by `repository_dispatch`. It uses JDK 17 (Temurin), Gradle, Android SDK build-tools `29.0.3`, and runs `./gradlew assembleRelease --stacktrace` in the checked-out upstream repository.
- CI creates `app/google-services.json`, `app/src/main/assets/client_secrets.json`, `app/src/main/java/exh/Version.kt`, and `app/src/main/res/raw/changelog_debug.xml` from secrets or run metadata before building. Keep these generated files and secrets out of this repository.
- Release packaging and filenames are defined in the workflow: the signed universal, `arm64-v8a`, `armeabi-v7a`, `x86`, and `x86_64` APKs are renamed, checksummed, and published as a GitHub release tagged with the workflow run number. Update all corresponding rename, checksum, and upload entries together.
- There is no repository-local build, test, lint, or typecheck command. Validate workflow changes by checking the YAML and, when possible, exercising the GitHub Actions workflow rather than attempting a local Gradle build.
- `.github/runner-files/ci-gradle.properties` is not referenced by the current workflow; do not assume its settings are applied to CI unless the workflow is changed to install or use it.
