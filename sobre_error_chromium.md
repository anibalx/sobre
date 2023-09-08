# Erro do Chromium
User namespace no kernel do Debian precisa ser abilitado
```
  sudo sysctl -w kernel.unprivileged_userns_clone=1
```
[Enable user namespaces in Debian kernel](https://superuser.com/questions/1094597/enable-user-namespaces-in-debian-kernel)
[How to enable user_namespaces in the kernel? (For unprivileged `unshare`.)](https://unix.stackexchange.com/questions/303213/how-to-enable-user-namespaces-in-the-kernel-for-unprivileged-unshare)
[Arch Wiki - Sysctl](https://wiki.archlinux.org/index.php/sysctl)
