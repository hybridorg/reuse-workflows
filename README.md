# reuse-workflows

## molecule workflow

```yaml
name: molecule_testing
on: [push]
jobs:
  run_molecule_tests:
    strategy:
      fail-fast: false
      max-parallel: 5
      matrix:
        distro:
          - image: centos
            tag: 8
          - image: ubuntu
            tag: noble
          - image: ubuntu
            tag: jammy
          - image: ubuntu
            tag: focal
          - image: ubuntu
            tag: bionic
          - image: debian
            tag: 11
          - image: debian
            tag: 12
          - image: debian
            tag: 13
          - image: fedora
            tag: 41
          - image: fedora
            tag: 42
    uses: hybridorg/reuse-workflows/.github/workflows/molecule.yml@main
    secrets: inherit
    with:
      distro_image: ${{ matrix.distro.image }}
      distro_tag: ${{ matrix.distro.tag }}
      working_directory: 'hybridadmin.fancy_console'

```

## build-push workflow

```yaml
name: build_push
on: [push]
jobs:
  run_molecule_tests:
    strategy:
      fail-fast: false
      max-parallel: 5
      matrix:
        distribution:
          - image: fedora
            version: "40"
            platform: "linux/amd64"
            tags: "40"
          - image: fedora
            version: "41"
            platform: "linux/amd64"
            tags: "41"
          - image: fedora
            version: "42"
            platform: "linux/amd64"
            tags: "42, latest"
    uses: hybridorg/reuse-workflows/.github/workflows/build_push.yml@main
    secrets: inherit
    with:
      distro_image: ${{ matrix.distro.image }}
      distro_tags: ${{ matrix.distro.tags }}
      distro_platform: {{ matrix.distro.platform }}
      distro_version: {{ matrix.distro.version }}
      repo_name: 'hybridadmin/ansible-fedora'
```
