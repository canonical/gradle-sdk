# Gradle SDK for Workshop

A development environment for Gradle projects. It provides versioned releases
of the Gradle build tool and persists packages to speed up builds across
workshop updates.

---

## Reference workshop

A minimal workshop:

```yaml
# workshop.yaml
name: gradle-app
base: ubuntu@24.04
sdks:
  - name: openjdk
    channel: 21/stable
  - name: gradle
    channel: 9/stable

actions:
  build: gradle build
  launch: gradle run
  test: gradle test
```

This demonstrates a basic Gradle build workflow.

> Note: The Gradle Workshop SDK requires a [Java Development Kit](https://jdk.java.net/) (JDK) installation with a suitable version to run. You can check the [compatibility matrix](https://docs.gradle.org/current/userguide/compatibility.html#compatibility) for more information.

---

## Using the SDK

### Prerequisites, project layout

1. The `openjdk` SDK (or other JDK installation) is required.
2. Your Gradle project should be in your project directory.
3. On launch, the SDK confugures `PATH`. No dependencies are pre-installed; Packages are downloaded during the first `gradle build` or `gradle run`.

### Build the project

Once the workshop is ready:

```bash
workshop shell
gradle build
```

The first build downloads packages into `~/.gradle/caches`, which is mapped to your host via the `gradle-cache` mount plug. Subsequent builds reuse cached packages.

To see where the Gradle cache is stored on the host:

```bash
workshop info
```

### Test and run

From within the workshop shell:

```bash
workshop shell
gradle test
gradle run
```

Use standard `gradle` and `./gradlew` commands; the toolchain behaves exactly as it would in a regular Gradle installation.

---

## Plugs (resources this SDK consumes)

### `gradle-cache`

- Interface: `mount`
- Workshop target: `/home/workshop/.gradle/cache`
- Purpose: Persists package downloads between workshop updates.

## Slots (resources this SDK provides)

This SDK doesn't define any slots.

---

## Documentation and guidance

- [Gradle official documentation](https://docs.gradle.org/current/userguide/userguide.html)
- [OpenJDK workshop SDK reference](https://github.com/canonical/openjdk-sdk)
- [Workshop documentation](https://ubuntu.com/workshop/docs/)

---

## Community and support

- Gradle community: [Gradle Community Forum](https://discuss.gradle.org/)
- Workshop forum: [Discourse](https://discourse.ubuntu.com/)
- Please review our [Code of Conduct](https://ubuntu.com/community/ethos/code-of-conduct)
  before participating.

---

## Contributions

All contributions, including code, documentation updates, and issue reports,
are welcome!

- See [CONTRIBUTING]([public-github-url]) for guidelines.
- Open issues or pull requests on the [official repository]([repo-url]).

---

## License and copyright

Copyright 2026 Canonical Ltd.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License version 2.1 (LGPLv2.1) as published by the Free Software Foundation.

Gradle is licensed under [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
