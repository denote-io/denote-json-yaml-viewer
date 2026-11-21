# JSON and YAML viewer

View JSON and YAML as a safe, local, keyboard-accessible structured tree.

This is an optional [Denote](https://github.com/denote-io/denote) plugin. Its
user guide is [guide.md](guide.md); Denote shows the same guide in
**Settings → Plugins**.

## Install

Enable **JSON and YAML viewer** from **Settings → Plugins** in Denote. Denote
downloads the release archive pinned in its built-in catalog, verifies its size
and SHA-256 digest, and only then loads the plugin in an isolated worker.

## Development

Use the Node.js version in `.node-version`.

```bash
npm ci
npm run typecheck
npm test
npm run check     # manifest, guide, and import boundaries
npm run package   # build, verify, and write .plugin-artifacts/denote.json-yaml-viewer-<version>.tgz
```

`npm run dev` rebuilds `.plugin-dev/denote.json-yaml-viewer.tgz` on every change. Load it
in Denote Development from **Settings → Plugins → Load local plugin archive**.
Disable the local plugin before loading rebuilt bytes with the same ID.

The build uses the [Denote plugin SDK](https://github.com/denote-io/denote-plugin-sdk)
and its `denote-plugin` command. It produces a single self-contained worker
bundle and a reproducible archive with fixed file modes, no timestamps, and LF
text. The pinned Vite and Rolldown versions keep archive bytes stable.

## Release

Published versions are immutable. To release a change:

1. Bump `version` in both `plugin.json` and `package.json`.
2. Merge to `main` with CI passing.
3. Run the **Release** workflow. It builds, verifies, and publishes
   `denote.json-yaml-viewer-<version>.tgz` as the `v<version>` release asset.
4. Update the plugin's entry in Denote's catalog to the new release so the
   application offers it.

## History

This plugin was developed in `plugins/json-yaml-viewer` of
[mbianchidev/denote](https://github.com/mbianchidev/denote), whose history for
this directory is preserved here. `releases.json` records every version
published from that repository, with its source commit there, original asset
URL, size, and SHA-256 digest.

[v0.1.4](https://github.com/denote-io/denote-json-yaml-viewer/releases/tag/v0.1.4) republishes the identical archive Denote
already offers (`5daab944e1d6d7c85e22a81bafcad3abb742303de9a2a2fc713c81ea96456422`, 66788 bytes),
built from source commit `75937a627d157f7698703485a5cb686cab9bb576` in
mbianchidev/denote. The source in this repository is unchanged from that commit.

CI rebuilds that version and checks it matches the published archive byte for
byte, so a source change cannot ship without a version bump.

## License

[MIT](LICENSE)
