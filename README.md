[![build-ublue](https://github.com/awebeer256/ublue-akmods/actions/workflows/build.yml/badge.svg)](https://github.com/awebeer256/ublue-akmods/actions/workflows/build.yml)

# ublue-os akmods

A layer for adding extra kernel modules to your image. Use for better hardware support and a few other features!

# Usage

Add this to your Containerfile to install all the RPM packages, replacing `RELEASE` with either `37` or `38`:

    COPY --from=ghcr.io/awebeer256/ublue-akmods:RELEASE /rpms/ /tmp/rpms
    RUN rpm-ostree install /tmp/rpms/ublue-os/*.rpm
    RUN rpm-ostree install /tmp/rpms/kmods/*.rpm

This example shows:
1. copying all the rpms from the akmods image
2. installing the ublue specific RPM, providing any extra repos and the akmod signing key
3. installing the kmods RPMs, providing the actual kmods built in this repo

The rpmfusion and extra repos provide dependencies which are required by the kmods RPMs.


# Features

Feel free to PR more kmod build scripts into this repo!

- ublue-os-akmods-addons - installs extra repos and our kmods signing key; install and import to allow SecureBoot systems to use these kmods <!-- - [v4l2loopback](https://github.com/umlaeute/v4l2loopback) - allows creating "virtual video devices" -->
- [xone](https://github.com/medusalix/xone) - xbox one controller USB wired/RF driver (akmod from [negativo17 steam repo](https://negativo17.org/steam/)
- [xpadneo](https://github.com/atar-axis/xpadneo) - xbox one controller bluetooth driver (akmod from [negativo17 steam repo](https://negativo17.org/steam/)

# Adding kmods

If you have a kmod you want to contribute send a pull request by adding a script using [build-kmod-wl.sh](https://github.com/ublue-os/akmods/blob/main/build-kmod-wl.sh) as an example.

# Verification

These images are signed with sisgstore's [cosign](https://docs.sigstore.dev/cosign/overview/). You can verify the signature by downloading the `cosign.pub` key from this repo and running the following command, replacing `RELEASE` with either `37` or `38`:

    cosign verify --key cosign.pub ghcr.io/awebeer256/ublue-akmods:RELEASE

