Wayland
Wayland is intended as a simpler replacement for X, easier to develop and maintain. GNOME and KDE are expected to be ported to it.

Wayland is a protocol for a compositor to talk to its clients as well as a C library implementation of that protocol. The compositor can be a standalone display server running on Linux kernel modesetting and evdev input devices, an X application, or a wayland client itself. The clients can be traditional applications, X servers (rootless or fullscreen) or other display servers.

Part of the Wayland project is also the Weston reference implementation of a Wayland compositor. Weston can run as an X client or under Linux KMS and ships with a few demo clients. The Weston compositor is a minimal and fast compositor and is suitable for many embedded and mobile use cases.