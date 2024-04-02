# rhel_image role

[![License: GPLv3](https://img.shields.io/badge/license-GPLv3-brightgreen.svg)](https://www.gnu.org/licenses/gpl-3.0)

Please see the collection main page for a higher level description.

## Configuration

Below are the role default values from defaults/main.yml:

<pre>
---
# Tasks
rhel_image_do_setup: true
rhel_image_do_build: true
rhel_image_do_cleanup: true
rhel_image_do_uninstall: false

# Setup
rhel_image_update_host: false
rhel_image_create_user: false
rhel_image_builder_user: image-builder
rhel_image_reboot_host: false

# Optional repository setup for Satellite/Capsule
# In case Image Builder was already installed the
# system will be rebooted to ensure correct usage
# See https://access.redhat.com/solutions/5773421
rhel_image_use_satellite: false
# Repo versions to enable using build host config
rhel_image_repo_versions:
#  - "{{ ansible_facts.distribution_major_version }}"
#  - "{{ ansible_facts.distribution_major_version }}.8"
# Custom repository configuration templates to copy
rhel_image_repo_templates:
#  - rhel-92.json.j2
#  - rhel-94.json.j2

# Blueprint
rhel_image_git_remote_repo: file:///tmp/rhel-image-blueprints.git
rhel_image_git_repo_checkout: master
rhel_image_local_repo_path: /tmp/blueprint-repo

# Build
rhel_image_blueprint: base-image
# This is on the build host
rhel_image_download_dir: /tmp/images
# Optional image filename to use instead of UUID
rhel_image_filename:
rhel_image_build_remove: true

# Image - only define needed options
rhel_image_output_type: qcow2
rhel_image_size_kb:
rhel_image_ostree_ref:
rhel_image_ostree_parent:
rhel_image_ostree_url:

# Fetch from build host
rhel_image_fetch_image: false
# This is where playbook runs
rhel_image_fetch_directory: /tmp
rhel_image_remote_delete: false
</pre>

## License

GPLv3+
