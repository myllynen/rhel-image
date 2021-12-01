# RHEL Image Builder Roles

[![License: GPLv2](https://img.shields.io/badge/license-GPLv2-brightgreen.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
[![License: GPLv3](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)](https://www.gnu.org/licenses/gpl-3.0)

Simple Ansible roles for building RHEL images with Image Builder.

## Quick Usage Example

```
vi base-image.toml
vi roles/image_builder_image_build/defaults/main.yml
ansible-playbook -i 192.168.122.123, -u root image_builder.yml
```

## License

GPLv2+
