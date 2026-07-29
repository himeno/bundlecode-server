# bundlecode-server

Remote extension host (REH) builds for [BundleCode](https://github.com/himeno/BundleCode), a personal fork of
[Visual Studio Code](https://github.com/microsoft/vscode).

This repository holds no source. It exists only so that the builds under
[Releases](../../releases) can be fetched without authentication, which is what
the SSH remote extension needs.

## Why this is needed

A remote SSH session downloads a server whose commit matches the client. Those
builds are published per fork, and BundleCode is not VS Code, so nothing
upstream serves a matching one. The builds here fill that gap.

Each release is tagged with the commit its client reports, so the URL template
below resolves on its own.

## Use

In `settings.json`:

```json
"remote.SSH.serverDownloadUrlTemplate": "https://github.com/himeno/bundlecode-server/releases/download/${commit}/bcode-reh-${os}-${arch}.tar.gz"
```

The server installs to `~/.bundlecode-server/bin/<commit>/` on the remote host.

Built for `linux-x64` and `linux-arm64`.

## Building these

From a BundleCode checkout at the matching commit:

```bash
npm run gulp vscode-reh-linux-x64-min      # compiles, then packages
npm run gulp vscode-reh-linux-arm64-min-ci # reuses the compile, packages only
```

Then add `LICENSE.txt` and `ThirdPartyNotices.txt` to each output directory and
tar it so that a single directory sits at the root — the install script extracts
with `--strip-components 1`.

## License

MIT, inherited from Visual Studio Code. `LICENSE.txt` and
`ThirdPartyNotices.txt` ship inside every archive.

Not affiliated with or endorsed by Microsoft.
