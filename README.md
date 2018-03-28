# PCF Pipelines - Tile Installs

This repository contains additional tasks that _extend_ the Pivotal supported [PCF Pipelines](https://github.com/pivotal-cf/pcf-pipelines) to support installing various tiles from scratch on a new foundation as well as supporting any tile configuration changes. The goal is to provide repeatability and auditability via tile configuration in version control and execution via Concourse.

## Usage

Unlike most Concourse pipeline repositories, this repository doesn't contain a complete pipeline that is ready to be fly'd. Each install-* directory contains three files:

- README.md - specific instructions on how to use the pipeline and what parameters are required.
- params.yml - all available tile parameters along with default values.
- pipeline-patch.yml - YAML patch file that contains the config-product task specific to the tile.

Generally all tile installation and configuration pipelines work the same. You use the [yaml-patch](https://github.com/krishicks/yaml-patch) CLI to add the tile specific pipeline-patch.yml ops file to the generic pipeline.yml file at the root of the repository. If you make any changes to the patch file or main pipeline.yml file you'll need to re-run yaml-patch to generate the new tile specific Concourse pipeline. Since generally all tile pipelines behave the same but with different parameters, this was done to reduce duplication.
