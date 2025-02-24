# pybamm-data

A repository for reproducibly storing data files used in [PyBaMM](https://github.com/pybamm-team/PyBaMM).

## Usage instructions

These instructions cover the following scenarios, that are intertwined with each other:

- for updating data files or adding new data files,
- and their subsequent usage in PyBaMM.

### Updating data files or adding new data files

1. To update an existing data file or to add a new data file, first, download all the data files from the latest release of this repository. This can be done by clicking on the latest release in the GitHub UI and downloading all the files. It is important to download all the files and not just the file you want to update, as these data files are versioned together with the repository's releases.

    As the number of data files is large and will accumulate over time, it is cumbersome to download all the data files manually. To automate this process, you can use the following command, which requires [the `gh` CLI](https://cli.github.com/) to be installed:

    ```bash
    gh release download TAG --repo https://github.com/pybamm-team/pybamm-data --dir DIR
    ```

    where `TAG` is the tag of the latest available release, and `DIR` is the directory where the data files will be downloaded.

2. Update the data files you want to change or add new data files, and compute their SHA-256 checksums using the `shasum --algorithm 256` or the `sha256sum` commands. For Windows (PowerShell) users, the `Get-FileHash <file> -Algorithm SHA256` command may be used.

> [!IMPORTANT]
> 3. Now, push an empty commit and tag it with a new version, and create a new release with the GitHub UI by uploading all the data files, including previous ones and updated ones. The version should be bumped according to [semantic versioning](https://semver.org/). The tag should be in the format `vX.Y.Z`, where `X`, `Y`, and `Z` are the major, minor, and patch versions, respectively. For example, if the latest release is `v1.2.3`, the new release should be `v1.2.4` if only data files are updated, or `v1.3.0` if new data files are added.

4. Next, the release note can be copied over from the previous release and modified accordingly. It should contain the following information:
    - The complete list of updated or added data files, along with their SHA-256 checksums.
    - If required, a brief description of the changes made to the data files for additional information and context about their inclusion.

> [!NOTE]
> version 1.0.1 did not conform to semantic versioning. The next version should be version 1.0.2 if files are updated, or version 1.1.0 if new files are added.

<!-- remove the above note after the next release here, whenever it comes -->

### Using data files in the PyBaMM repository

The next part is to use the release you just created. To do this:

1. Bump the version with the `pybamm-data` release you just created in https://github.com/pybamm-team/PyBaMM/blob/725a42cadbe8d3d233cd4990a0004b647aedec43/src/pybamm/pybamm_data.py#L83 in the
PR that you are working on.

2. If new files were added or existing files were updated in the new release, update the SHA-256 checksums in the registry in the same file.
