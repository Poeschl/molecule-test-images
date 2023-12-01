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

## CI Image

To be able to have working podman molecule environment a container images is also available.
It already contains a pre-installed python, pipenv environment and the ansible-galaxy podman collection.

It can be used like that in GitHub Actions:

```yaml
jobs:
  build:
    name: Check with molecule
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/poeschl/molecule-test-image:ci
```

See also the [living example](https://github.com/Poeschl/ansible-collection/blob/main/.github/workflows/molecule-tests.yaml).
