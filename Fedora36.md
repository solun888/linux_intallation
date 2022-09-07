# Minimal Installation of Fedora 36

---

1. Download "Everything" Installer [Fedora Installer Link](https://alt.fedoraproject.org/)


1. DNF Configuration [Reference](https://dnf.readthedocs.io/en/latest/conf_ref.html)
```bash
sudo nano /etc/dnf/dnf.conf

fastestmirror=True
max_parallel_downloads=10
defaultyes=True
keepcache=True
```

