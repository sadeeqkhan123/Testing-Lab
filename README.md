# hereditary-exome-v1

Germline SNV/indel calling for the hereditary cancer exome service at
**Northfield Molecular Diagnostics** (demonstration laboratory).

Snakemake · GATK best practices (BWA-MEM → MarkDuplicates → BQSR →
HaplotypeCaller → joint genotyping → hard filtering) · GRCh38.

Current release: **v3.2.0** · Validated baseline: **v3.1.0** ([CHANGELOG](CHANGELOG.md))

## Layout

```
workflow/   Snakefile, rules, per-rule conda environments
config/     config.yaml, samples.tsv, units.tsv
aver.yaml   validation settings for the Aver CLI (optional)
```

That is the whole repository. Run it with:

```bash
snakemake --use-conda --cores 16
```

## How this repository works with Aver

Aver does not need a special repository. **Labs connect the pipeline repo they
already have** — Aver reads it (read-only, https), fingerprints every tool,
container digest, conda environment and parameter into a snapshot, and
benchmarks it against public GIAB reference material. No patient data is
involved anywhere: the sample sheets in `config/` refer to public test reads
only, and benchmarking always uses NIST reference samples.

The minimum Aver needs per engine:

| Engine | Minimum in the repo |
|---|---|
| Snakemake | a `Snakefile` (or `workflow/Snakefile`) plus your config |
| Nextflow | `main.nf` and `nextflow.config` |
| Neither | register a container image + parameter file manually instead |

Good practice that makes validation sharper (all optional):

- **Tag releases** (`v3.1.0`, `v3.2.0`) — baselines and drift then map to versions.
- **Pin versions**: exact conda versions (`samtools ==1.10`, not `=1.10`) and
  container digests, not tags. Aver flags whatever is left unpinned.
- **`aver.yaml`** in the root lets anyone run `aver resolve` / `aver benchmark`
  from a clone with the lab's settings.

```bash
pip install aver-cli
aver resolve      # dependency snapshot of this checkout
aver benchmark    # GIAB HG002 benchmark, chr20
```

---

*Demonstration repository for a fictional laboratory.* Pipeline derived from
[snakemake-workflows/dna-seq-gatk-variant-calling](https://github.com/snakemake-workflows/dna-seq-gatk-variant-calling)
(v2.1.1, MIT — see [LICENSE](LICENSE)).
