# Li-MACE: Battery Machine Learning & Lithium DFT

**DFT benchmarks and machine-learned interatomic potentials for lithium on graphene-based battery materials.**

How do graphene defects change lithium binding, and where does MACE fine-tuning
improve atomic forces? Li-MACE brings together DFT reference calculations,
trained models, and configuration-resolved benchmarks to answer these questions.

**[Download Supplementary Data (21 MB)](https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT/releases/download/paper-v1.0/Reproducibility_Archive.zip)** |
[Release and checksum](https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT/releases/tag/paper-v1.0) |
[Explore the data](submission_data/README.md) |
[Model checkpoints](submission_data/models/README.md)

![DFT lithium adsorption energies and MACE force benchmarks across graphene defect environments](manuscript/figures/scientific_summary_strengthened.png)

Research accompanying **Machine-learning interatomic potentials for battery
materials: Defect-dependent lithium adsorption and local transferability on
graphene**, by Yuhan Sun and Xiao Huang. Accepted in *Computational Materials
Science*. Both authors contributed equally.

## What the study finds

- **Defect-dependent lithium binding.** Across 15 fixed-geometry DFT adsorption
  calculations, all sampled defective and Si-containing placements bind Li
  more strongly than the sampled pristine placements. The monovacancy gives
  the strongest sampled binding.
- **Force improvements across five environments.** Fine-tuning reduces pooled
  force RMSE from 450.0 to 267.5 meV per angstrom on 25 independently defined
  perturbations, a 40.6% reduction, with improvements in every structural family.
- **Structure-specific training targets.** Direct DFT tests of MD snapshots
  resolve the contrast between Si-containing environments and strained carbon
  near monovacancies, identifying concrete configurations for further labeling.

The five environments are pristine graphene, monovacancy, divacancy,
Stone-Wales, and a local Si4-on-graphene motif. The figure shows adsorption
energies, family-resolved force errors, displacement-amplitude dependence, and
the finite-temperature snapshot comparison.

## Download the paper archive

The release asset is the **exact Supplementary Data ZIP prepared for the
article**, preserved byte for byte. It is publicly downloadable without a
GitHub account. For journal production, use `Reproducibility_Archive.zip` from
the release assets rather than GitHub's automatically generated source ZIP.

```bash
curl -fL -O https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT/releases/download/paper-v1.0/Reproducibility_Archive.zip
curl -fL -O https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT/releases/download/paper-v1.0/SHA256SUMS.txt
sha256sum -c SHA256SUMS.txt
unzip Reproducibility_Archive.zip
cd Li-vasp_reproducibility_fdf568c
```

On macOS, use `shasum -a 256 -c SHA256SUMS.txt` for the checksum step.

The archive is pinned to source commit
[`fdf568c`](https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT/tree/fdf568c664115c6535c480374d6a97b032cdef79).
Its original directory name is retained. README improvements on `main` do not
change this paper-specific snapshot.

## Verify the results package

From the extracted archive root, run these checks with Python 3.10 or newer:

```bash
python review_revision/build_fair_submission_data.py --check
python review_revision/verify_resubmission_science.py --archive-only
python review_revision/static_check_manuscript.py --archive-only
```

These CPU-only checks validate the data manifest, model hashes, dataset sizes,
convergence records, and agreement between numerical evidence and manuscript
values. They use the distributed results and do not launch simulations or
submit scheduler jobs.

For the current development checkout:

```bash
git clone https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT.git
cd Li-MACE-Battery-Machine-Learning-Li-DFT
```

## Data and models

| Resource | Contents |
| --- | --- |
| [DFT datasets](submission_data/datasets/) | 273 configurations, original and group-held-out split definitions |
| [Relaxed structures](submission_data/structures/relaxed/) | Five reference geometries |
| [Adsorption references](submission_data/results/d3_site_adsorption_energies.csv) | 15 PBE-D3(BJ) calculations with slab dipole corrections |
| [Independent force benchmark](submission_data/results/balanced_perturbation_force_summary.csv) | 25 predefined perturbations, five per family |
| [MD force-validation configurations](submission_data/results/high_displacement_dft.extxyz) | Nine configurations with DFT force labels |
| [Extended snapshot evidence](submission_data/results/extended_snapshot_dft_evidence.csv) | Seven additional DFT calculations |
| [Trained MACE models](submission_data/models/README.md) | Five checkpoints, their roles, sizes, and SHA256 hashes |
| [Analysis and plotting](review_revision/) | Scripts for benchmarks, figures, and numerical verification |
| [Article source](manuscript/li_mace_graphene_draft.tex) | Main manuscript, including all six figures and eight tables |

The foundation model is MACE-MPA-0. Its official download and exact checksum,
along with the MACE versions used for fine-tuning, are documented in the
[model guide](submission_data/models/README.md). Model inference requires a
compatible MACE/PyTorch environment; load serialized checkpoints only from
trusted sources.

All scientific figures and summary tables are in the main article.
Supplementary Data supplies the underlying configurations, labels, models,
tables, and code. Adsorption comparisons use fixed geometries; path scans
describe energy spans, and MD traces describe finite-window displacement.

## Cite the work

Yuhan Sun and Xiao Huang. *Machine-learning interatomic potentials for battery
materials: Defect-dependent lithium adsorption and local transferability on
graphene*. Computational Materials Science, accepted, 2026.

For a reproducible software/data reference, cite the
[paper-v1.0 release](https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT/releases/tag/paper-v1.0)
and its source commit. Bibliographic details will be updated when the final
article DOI is available.

## Licenses and reuse

Analysis and workflow code: [MIT](LICENSE).
Curated data and author-trained checkpoints: [CC BY 4.0](submission_data/DATA_LICENSE.md).

Licensed VASP potentials and large raw runtime files are not part of the
distribution. See the [archive manifest](REPRODUCIBILITY_ARCHIVE_MANIFEST.md)
for included files and provenance. Open an
[issue](https://github.com/xiaohuang-6/Li-MACE-Battery-Machine-Learning-Li-DFT/issues) for questions about the
distributed code or data.
