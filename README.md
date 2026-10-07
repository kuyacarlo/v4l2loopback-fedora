# v4l2loopback Fedora packaging

Fedora packaging for the upstream [`v4l2loopback`](https://github.com/v4l2loopback/v4l2loopback) virtual Video4Linux loopback device tools and DKMS module.

This is a packaging repository. Do **not** run install, DKMS registration, or module-loading commands as part of repository verification on a workstation; those actions can touch host kernel/module state.

## Contents

- `v4l2loopback.spec` — RPM spec for the userspace utilities and `v4l2loopback-dkms` subpackage.
- `build.sh` — helper that fetches sources, builds an SRPM with Mock, then either rebuilds locally or submits to COPR when a COPR name is supplied.

## Safe local checks

These checks validate packaging metadata without installing a driver or touching running services:

```sh
rpmspec -q --srpm v4l2loopback.spec
rpmspec -q --requires v4l2loopback.spec
bash -n build.sh
```

A full RPM build requires Fedora packaging tools (`spectool`, `mock`, `rpmspec`) and a configured Mock environment. Run it only when you intentionally want a local package build:

```sh
./build.sh
```

To submit the built SRPM to COPR, pass the COPR project name. This performs a remote build submission and is intentionally not part of safe local finalization:

```sh
./build.sh <copr-project-name>
```

## Current package target

- Upstream source: `v4l2loopback`
- Spec version: `0.15.3`
- Package split: main userspace tools plus `v4l2loopback-dkms` for module source/DKMS registration

## License

The packaging repo carries the upstream GPLv2 license in [`LICENSE`](LICENSE).
