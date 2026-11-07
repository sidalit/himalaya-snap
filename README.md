<div align="center">

<img src="snap/gui/himalaya.png" alt="Himalaya logo" width="128" />

# Himalaya

**Manage your emails from the command line.**

[![himalaya](https://snapcraft.io/himalaya/badge.svg)](https://snapcraft.io/himalaya)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64, arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Himalaya](https://github.com/pimalaya/himalaya), a command-line email client for IMAP, SMTP, JMAP, Gmail, Microsoft Graph, Maildir and mbox.

</div>

---

## Getting Started

<a href="https://snapcraft.io/himalaya"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install himalaya
himalaya
```

Without a configuration, `himalaya` starts a wizard that discovers your provider's servers and prints a TOML account. Save it to the configuration file below, then run `himalaya envelope list` and `himalaya message read <id>`.

## Configure

There are no `snap set` options. Himalaya reads `~/snap/himalaya/current/.config/himalaya/config.toml`; see the upstream [config.sample.toml](https://github.com/pimalaya/himalaya/blob/master/config.sample.toml). In the configuration, `~` means `~/snap/himalaya/current`, so use absolute paths for folders outside the snap.

| Setting | Accepted values | Default |
| --- | --- | --- |
| `downloads-dir` | An absolute folder path, such as `/home/alice/Downloads` | The snap's private `/tmp` |
| `imap.sasl.plain.password.command` | A command that prints the password, such as `"secret-tool lookup himalaya example"` | Not set |

To keep passwords in your desktop keyring, connect the interface and store each password once:

```bash
sudo snap connect himalaya:password-manager-service
himalaya.secret-tool store --label "Himalaya example" himalaya example
```

For Maildir or mbox folders on removable storage:

```bash
sudo snap connect himalaya:removable-media
```

## Limitations

- Password and token commands run inside the snap. Only the included `secret-tool` is available; host programs such as `pass`, `gopass` or `ortie` are not.
- Maildir and mbox folders must be in a normal folder under your home directory or on connected removable storage. Hidden folders directly under your home directory, such as `~/.mail`, are not accessible.
- A configuration in the host's `~/.config/himalaya` or `~/.himalayarc` is not read.

## Build

```bash
git clone https://github.com/sidalit/himalaya-snap.git
cd himalaya-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/himalaya-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/pimalaya/himalaya/issues).

## License

Snap packaging: [MIT](LICENSE).
