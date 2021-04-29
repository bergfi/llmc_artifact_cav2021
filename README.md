# LLMC Artifact for CAV2021

This repository contains all scripts and files related to the LLMC Artifact for CAV2021. To recreate the artifact, it is enough to clone this repository to `$HOME/artifact` and install the requirements:
- cmake 3.19
- llvm 11
- git
- darcs
- boost
- python 3
- libffi
- clang
- googletest
- graphviz
- time
- figlet
- python-pip
- python-yaml
- python packages: pandas, sqlite3

On Arch Linux this would be:
```
git clone https://github.com/bergfi/llmc ~/artifact
pacman -S cmake llvm git darcs boost python libffi clang gtest graphviz time figlet python-pip python-yaml
pip install pandas
pip install sqlite3
```

## Included commands

- `help`: print a short help page on how to invoke various commands to evaluate the artifact
- `run`: execute various tests. By default, runs a quick test suite that takes 2-4 hours.
- `show`: print all results so far
- `prepare`: compile binaries from source. Not needed, as binaries are included.

## Run the artifact on cases outside the artifact

The LLMC version included in the artifact can be executed on any LLVM IR file. As explained in the paper, it currently needs to assume that a static analysis pass has been done on the LLVM IR file that annotates memory instructions on whether they are provably thread-local or not. This needs to be enabled using the command line argument `--ll2dmc.assume_nonatomic_collapsable=1`.

A short summary of the command line interface to LLMC:
`llmc [OPTIONS] [LLVM IR FILE]`

`OPTIONS` can be:
- `-m SEARCHCORE`, where `SEARCHCORE` can be any of `singlecore_simple` or `multicore_bitbetter`
- `-s STATESTORAGE`, where `STATESTORAGE` can be any of `dtree`, `treedbsmod`, `treedbs_cchm`, `cchm` or `stdmap`
- `--threads N`, where `N` is the number of model-checking threads to use
- `--storage.hashmap_scale=N`, meaning the underlying hash map of any storage container will have 2^N elements
- `--ll2dmc.assume_nonatomic_collapsable=B`, B=1 enables the assumption that non-atomic memory operations are thread-local (see above)

For a more detailed description on how to execute LLMC, we refer to its [README.md](https://github.com/bergfi/llmc)
