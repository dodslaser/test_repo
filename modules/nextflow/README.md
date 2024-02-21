# Nextflow module for Cellophane

Module providing convenient access to functionality for launching NextFlow pipelines (particularly nf-core) from runners via SGE.

## Configuration

Option                      | Type | Required | Default  | Description
----------------------------|------|----------|----------|-------------
`nextflow.threads`          | int  |          | 2        | SGE slots the NextFlow main process
`nextflow.config`           | str  |          |          | Nextflow config file
`nextflow.profile`          | str  |          |          | Config profile(s) to use
`nextflow.ansi_log`         | bool |          | false    | Enable ANSI logging
`nextflow.nf_module`        | str  |          | nextflow | NextFlow envmodule to load
`nextflow.java_module`      | str  |          | java     | Java envmodule to load

# Functions

```
nextflow(
    main: Path,
    *args,
    config: cfg.Config,
    env: dict[str, str] = {},
    log: Path|None = None,
    report: Path|None = None,
    workdir: Path|None = None,
    nf_config: Path|None = None,
    ansi_log: bool = False,
    resume: bool = False,
    **kwargs,
) -> multiprocessing.Process:
```

Launch the NextFlow pipeline specified by `main`. Environment variables can be passed using `env`. Logs will be written to the path specified by `log` or discarded if it is None. If `report` is specified an HTML execution report will be written here. The NextFlow working directory can be specified by `workdir`. The `resume` parameter allows NextFlow execution to be resumed (assuming the output prefix is specified so that output is placed in the same location as a previous run) 

Additional `**kwargs` will be passed to `cellophane.sge.submit`

## Mixins

`NextflowSamples`

```
nfcore_samplesheet(self, *_, location: str | Path, **kwargs) -> Path:
```
Write an nf-core compatible sample sheet at `location`. Any `**kwargs` will be added as columns. Values in `**kwargs` may be strings (same will be added to all samples) or a `sample.id -> value` mapping, in which case the value for each sample cn be assigned individually.  

