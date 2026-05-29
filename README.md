# Disassembly Datasets for Coreutils

This dataset was created and published for the evaluation of the paper *Neurosymbolic Disassembly*.

## Description

The dataset is based on GNU Coreutils v9.9. The specific repository commits and build scripts used to generate this data can be found at the following links:

* [coreutils-arm-gcc](https://github.com/Q1IQ/coreutils-arm)
* [coreutils-arm-llvm](https://github.com/gdjs2/coreutils-arm-llvm)
* [coreutils-mips-gcc](https://github.com/gdjs2/coreutils-mips)
* [coreutils-mips-llvm](https://github.com/gdjs2/coreutils-mips-llvm)

**Note:** You do not need to check or clone these repositories if you only intend to use the pre-built dataset.

## Repository Structure

The directory is organized as follows:

```bash
.
├── LICENSE
├── README.md
├── arm32-gcc
│   ├── labels
│   ├── nonstripped
│   └── stripped
├── arm32-llvm
│   ├── labels
│   ├── nonstripped
│   └── stripped
├── mips-gcc
│   ├── labels
│   ├── nonstripped
│   └── stripped
└── mips-llvm
    ├── labels
    ├── nonstripped
    └── stripped
```

* **Top-level directories** (e.g., `arm32-gcc`, `mips-llvm`) specify the target architecture and the compiler used to build the Coreutils binaries.
* **Second-level directories** categorize the files for each build:
    * `labels/`: Memory labels for each binary, serving as the ground truth.
    * `nonstripped/`: The compiled binaries without stripping. 
    * `stripped/`: The stripped compiled binaries.
    
You can choose to use either the stripped or nonstripped binaries as input depending on your evaluation needs.

## Ground Truth Format

All ground truth files (located under the `**/labels/` directories) are provided as comma-separated values (`.csv`) files.

Each CSV contains four columns: `address`, `raw bytes`, `instruction`, and `ground_truth`.

Since all ARM32 and MIPS binaries in this dataset are 4-byte aligned, each row represents a 4-byte memory block starting at the specified `address`.

* **`raw bytes`**: The raw byte values stored at this specific 4-byte memory location.
* **`instruction`**: The decoded assembly instruction corresponding to this address. If the bytes cannot be successfully decoded, this field is marked as *invalid*.
* **`ground_truth`**: A label indicating the true classification of the memory block, where *0* represents actual code and *1* represents data.

## Citation

If you use this dataset in your research, please consider citing our work:

```bibtex
@inproceedings{xiao2026neurosymbolic,
  author    = {Xiao, Zhaoqi and Fu, Yeqi and Wijayadi, Lambang Akbar and Liang, Zhenkai and Yin, Heng},
  title     = {Neurosymbolic Disassembly},
  booktitle = {Proceedings of the 2026 ACM SIGSAC Conference on Computer and Communications Security (CCS '26)},
  year      = {2026},
  month     = {November},
  publisher = {Association for Computing Machinery},
  address   = {The Hague, Netherlands},
  note      = {To appear}
}