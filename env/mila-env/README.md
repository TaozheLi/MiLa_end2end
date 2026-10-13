# MiLA end-to-end environment export

Snapshot dated 2026-10-13 from running container docker-uniad-run-261b60597e6b, image uniad-mila:cuda118.

Python 3.9.18; Ubuntu 20.04.6; CUDA toolkit 11.8; PyTorch 2.0.1+cu118; mmcv-full 1.6.1; mmdet 2.26.0; mmdet3d 1.0.0rc6.

Observed /opt/conda size: approximately 6.1 GiB, including caches. Excludes system CUDA, code, datasets and weights. Server installation size may differ.

## Recreate on a Linux server

Preferred Conda snapshot:

```bash
PIP_EXTRA_INDEX_URL=https://download.pytorch.org/whl/cu118 conda env create -f environment.yml
conda activate mila-e2e
```

Alternative Python package snapshot:

```bash
conda create -n mila-e2e python=3.9.18 pip=23.3.2
conda activate mila-e2e
python -m pip install -r requirements.txt
```

## Files and limitations

- environment.yml preserves Conda and pip versions, removing the machine-specific prefix and Conda build pins.
- requirements.txt replaces local Conda build paths with version pins and excludes Conda-management packages. Includes the PyTorch CUDA 11.8 wheel index.
- requirements.raw.txt is an archival pip freeze; local build paths are not portable.
- packages.json records installed versions/source metadata.
- system-info.txt records OS, CUDA, sizes, and existing pip dependency conflicts.

A fresh server installation has not been tested. Existing pip dependency conflicts are preserved in this snapshot; inspect system-info.txt. MMCV and other CUDA extensions may need source builds or custom wheels matching PyTorch 2.0.1 and CUDA 11.8. Version pins do not capture patched source or binary build settings. Rebuilding extensions requires compatible CUDA development tools and a compiler; GPU execution requires a compatible server NVIDIA driver.

Transfer MiLA/UniAD project source, project CUDA extensions, datasets and weights separately. These exports contain package specifications only. Docker is not required to use these files.
