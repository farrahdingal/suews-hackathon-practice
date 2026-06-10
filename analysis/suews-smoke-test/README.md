# SUEWS smoke test

This folder records the practice SUEWS run used to check that the hackathon
tooling works end to end.

## What was run

- Tooling: `suews` / `suews-mcp` installed in a local workspace Python
  environment for this setup.
- SUEWS/SuPy version: `2026.6.5`.
- Starter case: `suews init --template simple-urban`.
- Validation: `suews validate --format json analysis/suews-smoke-test/sample_config.yml`.
- Simulation: `suews run analysis/suews-smoke-test/updated_sample_config.yml`.
- Diagnostics: `suews diagnose --format json analysis/suews-smoke-test`.

## Result

The run completed and wrote:

- `Output/KCL1_2012_SUEWS_60.txt`
- `Output/KCL_SUEWS_checkpoint.json`

The output summary over 8,784 hourly steps was:

| Variable | Mean | Min | Max | Missing |
| --- | ---: | ---: | ---: | ---: |
| QN | 44.76 | -83.80 | 646.98 | 0.0% |
| QH | 88.76 | -40.82 | 339.70 | 0.0% |
| QE | 27.58 | 1.70 | 195.34 | 0.0% |
| T2 | 11.91 | -5.24 | 30.40 | 0.0% |
| RH2 | 69.33 | 18.75 | 98.16 | 0.0% |

## Caveats

This is a demo-level smoke test using the bundled KCL/London sample forcing and
site settings. It proves the SUEWS pipeline runs locally, but it is not a
hackathon-city analysis and should not be interpreted as a heat-risk result.

The diagnostic report found no fatal failures. It did keep one warning about
mean energy-balance closure residual, so this run should be treated as a setup
check only.
