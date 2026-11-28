# pkg-mate-desktop (Menta Linux)

Debian packaging of mate-desktop 1.29.3 (from debian-mate-team/mate-desktop on
Salsa, 1.28.2-1). Builds: mate-desktop, mate-desktop-common, libmate-desktop-2-17t64,
libmate-desktop-dev, libmate-desktop-doc, gir1.2-matedesktop-2.0,
mate-wayland-protocols.

Versioning: `<upstream>-<debian rev>mentaN`, e.g. `1.29.3-1menta1`; bump with `dch -i`.

## Wayland

Since 1.29.3 upstream contains the Wayland monitor information, per-monitor
backgrounds and the MATE Wayland protocols (PR #722), so the downstream patch
`0001_wayland-monitor-info.patch` is gone. debian/rules passes `-Dwayland=enabled`,
so configuration fails instead of silently skipping Wayland support.

The protocol XML files and `mate-wayland-protocols.pc` are shipped by the
architecture-independent binary package `mate-wayland-protocols`. Earlier Menta
builds (1.29.1-1menta2 .. 1.29.2) shipped them in `libmate-desktop-dev`;
`mate-wayland-protocols` Breaks/Replaces `libmate-desktop-dev (<< 1.29.3-1menta1~)`
and `libmate-desktop-dev` Depends on it.

Everything later in the chain (mate-settings-daemon, mate-control-center,
mate-panel, ...) must be configured fresh against this build.

## Runtime workaround

The background settings dialog (mate-control-center) is not part of any
upstream PR yet, so the per-monitor background handling can misbehave. Owner's
runtime workaround (NOT set in packaging):

    gsettings set org.mate.background draw-background false

CI builds on every push to `master`; pushing a tag `menta/<version>` also
publishes the .debs as a GitHub release.
