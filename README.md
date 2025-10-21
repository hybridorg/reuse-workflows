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
