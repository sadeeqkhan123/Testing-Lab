# Changelog — hereditary-exome-v1

## v3.2.0 — 2026-09-18

- samtools environment updated (`=1.10` → `=1.12`) for the htslib CRAM fix
  flagged by IT security review.
- MultiQC report generation pinned to the shared container image used by the
  QC team. **TODO(QC): replace `:latest` with a digest before the next release.**

## v3.1.0 — 2026-06-12 (validated baseline)

- Baseline release validated under SOP-MOL-014.
- Joint genotyping and hard-filter thresholds per GATK best practices.
- Per-rule conda environments; wrappers at release 0.74.0.

## v3.0.2 — 2026-04-03

- Read-group handling fix for multi-lane samples.

## v3.0.0 — 2026-02-19

- Migration of the legacy bcbio pipeline to Snakemake.
