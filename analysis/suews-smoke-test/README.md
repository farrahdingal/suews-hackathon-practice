# SUEWS smoke test

This folder records the practice SUEWS run used to check that the hackathon
tooling works end to end.

## What was run

- Tooling: `suews` / `suews-mcp` installed in a local workspace Python
  environment for this setup.
- SUEWS/SuPy version: `2026.6.5`.
- SUEWS agent checks: `inspect_config`, `assess_readiness`,
  `validate_config`, `diagnose_run`, and `summarise_run`.
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

## Assumptions still from the sample case

The SUEWS agent readiness check marked the case as not ready for site-specific
science because three site-defining inputs are still from the bundled sample:

| Sample assumption | Current value | Why it matters |
| --- | --- | --- |
| Location | KCL/London, lat `51.51`, lon `-0.12`, altitude `10.7`, timezone `0.0` | This controls sun angle and radiation timing, so it affects net radiation and the heat balance. |
| Land cover | paved `0.43`, buildings `0.38`, evergreen trees `0.00`, deciduous trees `0.02`, grass `0.03`, bare soil `0.00`, water `0.14` | These fractions weight albedo, emissivity, storage heat, evaporation, and sensible heat. |
| Weather forcing | `Kc_2012_data_60.txt` | This supplies incoming radiation, air temperature, humidity, wind, and rain for the run. |

Readiness level: **Level 1 - demo**. It is good evidence that the tool works,
but not evidence about the real hackathon city.
