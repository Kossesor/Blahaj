# Version and release layout

The repository currently keeps one branch per Minecraft version. A release is
assembled from those branches; the branches are not merged into one build.

The `Build release artifacts` workflow is run manually from GitHub Actions. It
checks out every supported branch, selects the required Java version, runs its
own Gradle build, and publishes all resulting jars to one GitHub Release.

Current branches include Fabric and NeoForge targets. There is no Quilt branch
in the refork yet, so Quilt artifacts are not included until a Quilt port is
added.

For a release:

1. Merge or push the changes to every version branch that should ship.
2. Open Actions → Build release artifacts → Run workflow.
3. Enter the mod version, such as `4.0.0`.
4. The workflow creates tag `v4.0.0` and attaches each branch's jars.

This is the safe first phase. Once the existing artifacts are reproducible, the
branches can be migrated to a Stonecutter-style common/platform layout. That
step shares source code while retaining small version-specific patches where
Minecraft APIs differ.
