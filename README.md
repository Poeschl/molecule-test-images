# Molecule Test Images

For automated molecule tests for ansible I use this images for an easy use in my ansible projects.

## Molecule Images

### Usage

The images are build automatically from the `main` branch.

Available OSes:

* `debian`
* `ubuntu`

Available facets

* `basic` - just a basic os installation with minimalistic tools
* `with_docker` - same as `basic` + docker and docker-compose install
* `with_podman` - same as `basic` + podman and podman-compose install

All combinations can be retrieved with the following way in your `molecule.yaml`.
The image has the pattern `{{ os }}-{{ facet }}` for its tags.

```yaml
platforms:
  - name: molecule-ubuntu
    image: ghcr.io/poeschl/molecule-test-image:${MOLECULE_OS:-ubuntu}-basic
    command: ${MOLECULE_DOCKER_COMMAND:-""}
    privileged: true
    pre_build_image: true
```

### Rootless user

To test you roles and playbooks with an non-root user you can use the user `rootless` with uid `1000`.

```yaml
provisioner:
  name: ansible
  connection_options:
    ansible_ssh_user: rootless
```

