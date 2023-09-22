# Conda-lock refresh GitHub Action

Regenerate fully reproducible conda-lock.yml files for conda environments.

## Usage

This GitHub Action is designed to be used with the
[`issue_comment`](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#issue_comment)
event, such that writing a comment that starts with `/condalock` in a Pull
Request triggers a refresh of the lockfile. See full working demo example at
https://github.com/weiji14/conda-lock-refresh-demo/blob/main/.github/workflows/conda-lock.yml.
However, it should be possible to use other types of workflow trigger events to
refresh the lockfile too (e.g. on `label` creation, or `schedule` runs).

Sample workflow step:

```
- name: Run conda-lock
  uses: weiji14/conda-lock-refresh@main
  with:
    file: "environment.yml"
    kind: "lock"
    mamba: true
    platform: "linux-64"
```

### Action inputs

See [action.yml](./action.yml).
These parameters should match the flags in the `conda-lock lock` command at
https://conda.github.io/conda-lock/cli/gen/#conda-lock-lock

| Parameter | Description | Default |
|:--:|:--|:--|
| `file` | Path to the conda environment specification(s) | environment.yml |
| `kind` | Kind of lock file(s) to generate [should be one of 'lock', 'explicit', or 'env'] | lock |
| `mamba` | Use the mamba solver [should be either 'true' or 'false'] | true |
| `platform` | The platforms to generate the lockfile for | linux-64 |


## References

### Original motivation

The discussion to create a reusable GitHub Action was discussed at:
- https://github.com/CryoInTheCloud/hub-image/issues/18
- https://github.com/pangeo-data/pangeo-docker-images/issues/414

### Prior work

Credits to the previous work done on pangeo-docker-images and CryoCloud.
- https://github.com/pangeo-data/pangeo-docker-images/pull/33
- https://github.com/CryoInTheCloud/hub-image/pull/5
