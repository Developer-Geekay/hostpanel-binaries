# hostpanel-binaries

Pre-vetted, standalone binary distributions and release assets used by HostPanel packages. Packages pull binaries directly from here during `on_install()` / `engine-install` instead of bundling large files or relying on host OS package managers (`apt`, `yum`).

---

## 📂 Directory Layout

```
hostpanel-binaries/
├── database/
│   ├── mongodb/
│   │   ├── aarch64/          # mongodb-linux-aarch64-8.0.4.tgz (89MB), mongosh-2.3.8-arm64.tgz (77MB), db tools (48MB)
│   │   └── x86_64/           # mongodb-linux-x86_64-8.0.4.tgz (94MB), mongosh-2.3.8-x64.tgz (78MB), db tools (52MB)
│   └── mysql/
│       ├── aarch64/          # mariadbd, mariadb client tools (ARM64)
│       └── x86_64/           # mariadbd, mariadb client tools (x86_64)
├── webserver/
│   ├── Apache/
│   │   ├── aarch64/          # httpd runtime
│   │   └── x86_64/           # httpd runtime
│   ├── Nginx/
│   │   ├── aarch64/          # nginx (1.26+)
│   │   └── x86_64/           # nginx (1.26+)
│   └── LightSpeed/
│       ├── aarch64/
│       └── x86_64/
├── php/
│   ├── aarch64/              # php-8.4, php-fpm-8.4 (and multi-versions)
│   └── x86_64/               # php-8.4, php-fpm-8.4 (and multi-versions)
├── ftp/
│   ├── aarch64/              # pure-ftpd, pure-pw
│   └── x86_64/               # pure-ftpd, pure-pw
└── wireguard/
    ├── aarch64/              # wg, wg-quick
    └── x86_64/               # wg, wg-quick
```

---

## 🚀 How It Works

1. **Direct Raw Binary Fetch** (for standard binaries under 50 MB):
   ```text
   https://raw.githubusercontent.com/Developer-Geekay/hostpanel-binaries/main/{category}/{package}/{arch}/{binary}
   ```
   *Example*:
   `https://raw.githubusercontent.com/Developer-Geekay/hostpanel-binaries/main/webserver/Nginx/aarch64/nginx`

2. **GitHub Releases** (for large server binaries like `mongod`, `mysqld`):
   ```text
   https://github.com/Developer-Geekay/hostpanel-binaries/releases/download/{package}-{version}/{binary}-{arch}
   ```
   *Example*:
   `https://github.com/Developer-Geekay/hostpanel-binaries/releases/download/mongodb-8.0.4/mongod-aarch64`

3. **Standalone Runtime Target Isolation**:
   All downloaded binaries extract into `/opt/hostpanel/runtimes/<pkg>/bin/` or `/opt/hostpanel/packages/<pkg>/bin/` with `0755` permissions, ensuring 100% isolation with zero host OS dependencies.

