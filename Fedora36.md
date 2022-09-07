# Minimal Installation of Fedora 36

---

1. Download **"Everything"** Installer [Fedora Installer Link](https://alt.fedoraproject.org/)


1. DNF Configuration [Reference](https://dnf.readthedocs.io/en/latest/conf_ref.html)

    ```sh
    sudo nano /etc/dnf/dnf.conf

    fastestmirror=True
    max_parallel_downloads=10
    defaultyes=True
    keepcache=True
    ```

1. System Update 
   
   ```sh
    sudo dnf update
    ```

1. Enable RPM Fusion 
    
    To enable access to both the free and the nonfree repository use the following command:

    Fedora with dnf:
    ```sh
    sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
    ```
