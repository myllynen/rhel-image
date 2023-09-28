# RHEL Image Builder Role

[![License: GPLv3](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)](https://www.gnu.org/licenses/gpl-3.0)

Ansible role for building RHEL images with Image Builder.

## Quick Usage Example

This role builds custom RHEL images with
[RHEL Image Builder](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/composing_a_customized_rhel_system_image/index).
The role uses a given image blueprint from a Git repository and either
stores results on the build host or fetches them to the local node.

The role allows for first setting a build host by installing the needed
packages and optionally creating a dedicated user (which will be part of
the _weldr_ group) for running Image Builder. Then, images can be built
using the superuser or the dedicated user with any given blueprint.

To install this collection from GitHub:

```
ansible-galaxy collection install git+https://github.com/myllynen/rhel-image,master
```

Next, in a blueprint repository customize an image blueprint:

```
vi base-image.toml
git commit -m "Update base-image" base-image.toml
git push
```

Then, create a [playbook](image_builder.yml) to use this role:

```
---
- name: Build RHEL image with Image Builder
  hosts: all
  become: true
  vars:
    rhel_image_git_remote_repo: file:///tmp/rhel-image-blueprints.git
    rhel_image_git_repo_checkout: master
    rhel_image_blueprint: base-image
    rhel_image_size_kb: 30720
    rhel_image_output_type: qcow2
    # This is on the build host
    rhel_image_download_dir: /tmp/images
    # Fetch from build host
    rhel_image_fetch_image: true
    # This is where playbook runs
    rhel_image_fetch_directory: /tmp
    rhel_image_remote_delete: true
  roles:
    - myllynen.rhel_image.rhel_image
```

See [the role README](roles/rhel_image/) for all the supported
parameters.

Finally, build the image on a build host:

```
ansible-playbook -i 192.168.122.123, image_builder.yml
```

## Disconnected Environments

By default RHEL Image Builder tries to fetch repository data from Red
Hat CDN. In case internet access is restricted and repositories are
available on a local Satellite or such, the repository configuration
for each distribution version used in images must be adjusted.

See [this RHKB article](https://access.redhat.com/solutions/5773421)
for details how to configure RHEL Image Builder to use a local
Satellite.

## See Also

See also
[https://github.com/myllynen/ansible-packer](https://github.com/myllynen/ansible-packer).

See also
[https://github.com/myllynen/rhel-ansible-roles](https://github.com/myllynen/rhel-ansible-roles).

See also
[https://access.redhat.com/solutions/5773421](https://access.redhat.com/solutions/5773421).

## License

GPLv3+
