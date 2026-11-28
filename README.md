# BST-280 group project

## Data preparation (`01_script/00_inspect.Rmd`)

### Data source
Processed RNA-seq data from Young et al. (2021), *npj Systems Biology and Applications*, Zenodo record [3960874](https://zenodo.org/records/3960874).

The authors' files are **not** in this repo. Download and unzip them next to the repo. 


Scripts find the data with `here::here("..", "00_Young2021_OpenDataCode", "TB PANDA")`.

### Input files used
| File | Contents | Use |
|---|---|---|
| `rdata/log2CPM.RData` | `log2CPM` (3,974 genes × 69 samples) and `log2CPM.rm.batch` (authors' batch-corrected) | PCA, heatmap, batch check |
| `rdata/dge.rdata` | DE results table (logFC, adj. P at 12/24/48 hr). No counts. | Comparing with our results later |

### Sample metadata
There is no separate sample sheet. The metadata is parsed from the sample names, e.g. `T10_24hr_exp8_rep2`:

| Field | Levels |
|---|---|
| treatment | DMSO, T4, T10 |
| time | 0hr, 12hr, 24hr, 48hr |
| experiment (batch) | exp6, exp8, exp9 |
| rep | rep1–rep6 |

### Design notes
- DMSO is only at 0 hr (n = 15). T4 and T10 each have 27 samples (12/24/48 hr × 3 experiments × 3 reps). Total: 69.
- There is no time-matched control, so time effects are measured against the 0 hr baseline.
- Each experiment has 6 samples per time point, except exp6, which has 3 at 0 hr.
- `log2CPM` and `log2CPM.rm.batch` have identical sample order.

### Output
A `meta` data frame (one row per sample) used by the downstream PCA and heatmap scripts.