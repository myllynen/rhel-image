# RHEL Image Builder Role

[![License: GPLv2](https://img.shields.io/badge/license-GPLv2-brightgreen.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
[![License: GPLv3](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)](https://www.gnu.org/licenses/gpl-3.0)

A simple Ansible role for building RHEL images with Image Builder.

## Quick Usage Example

This role builds custom RHEL images with
[RHEL Image Builder](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/composing_a_customized_rhel_system_image/index).
The role uses a given image blueprint from a Git repository and
stores results on the build host.

First, install this role:

```
mkdir roles
cat << EOF > roles/requirements.yml
---
roles:
  - src: https://github.com/myllynen/rhel-image.git
    type: git
    version: master
EOF
ansible-galaxy role install -p roles -r roles/requirements.yml
```

Next, on a blueprint repository customize an image blueprint:

```
vi base-image.toml
git commit -m "Update base-image" base-image.toml
git push
```

Then, create a [playbook](./image_builder.yml) to use this role:

```
---
- name: Build RHEL image with Image Builder
  hosts: all
  become: true
  vars:
    create_user: false
    git_remote_repo: file:///tmp/rhel-image-blueprints.git
    git_repo_checkout: master
    image_blueprint: base-image
    image_size_kb: 20480
    image_output_type: qcow2
    image_download_dir: /tmp/images
  roles:
    - rhel-image
```

See [defaults/main.yml](defaults/main.yml) for all the supported
parameters.

Finally, build the image on a build host:

```
ansible-playbook -i 192.168.122.123, -u root image_builder.yml
```

## See Also

See also
[https://github.com/myllynen/ansible-packer](https://github.com/myllynen/ansible-packer).

See also
[https://github.com/myllynen/rhel-ansible-roles](https://github.com/myllynen/rhel-ansible-roles).

## License

GPLv2+
