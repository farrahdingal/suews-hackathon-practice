# SUEWS Agent Smoke-Test Report

Date: 2026-06-10

## Outcome

Run status: completed

Readiness: Level 1 - demo

This was a small setup check using the SUEWS agent tooling and the SUEWS CLI.
The case uses the packaged KCL/London sample configuration and forcing data, so
it proves the toolchain works but is not a site-specific or hackathon-city
result.

## Commands and agent checks used

```bash
suews init --template simple-urban --format json analysis/suews-smoke-test
suews run analysis/suews-smoke-test/updated_sample_config.yml
suews diagnose --format json analysis/suews-smoke-test
```

SUEWS agent tools used:

- `read_knowledge_manifest`
- `inspect_config`
- `assess_readiness`
- `validate_config`
- `diagnose_run`
- `summarise_run`

## Evidence

- `read_knowledge_manifest` reported SUEWS/SuPy `2026.6.5`, schema `2026.5`,
  and SUEWS source evidence commit `9dae7a8`.
- `inspect_config` reported site `KCL`, latitude `51.51`, longitude `-0.12`,
  and forcing file `Kc_2012_data_60.txt`.
- `assess_readiness` reported `ready: false` because location, land cover, and
  forcing are still sample defaults.
- `validate_config` reported the updated YAML is structurally valid with
  `error_count: 0`.
- `suews run` completed with `SUEWS run successfully done!`.
- `diagnose_run` reported 3 passes, 1 warning, and 0 failures.
- `summarise_run` reported 8,784 output time steps.

## Key summary values

| Variable | Mean | Min | Max | Missing |
| --- | ---: | ---: | ---: | ---: |
| QN | 44.76 | -83.80 | 646.98 | 0.0% |
| QH | 88.76 | -40.82 | 339.70 | 0.0% |
| QE | 27.58 | 1.70 | 195.34 | 0.0% |
| T2 | 11.91 | -5.24 | 30.40 | 0.0% |
| RH2 | 69.33 | 18.75 | 98.16 | 0.0% |

## Assumptions still from the sample case

| Sample assumption | Current value | Role in SUEWS | Risk |
| --- | --- | --- | --- |
| Location | KCL/London: lat `51.51`, lon `-0.12`, altitude `10.7`, timezone `0.0` | Controls solar geometry and timing of radiation. | The model is simulating London's sun and timing, not the hackathon city. |
| Land cover | paved `0.43`, buildings `0.38`, evergreen trees `0.00`, deciduous trees `0.02`, grass `0.03`, bare soil `0.00`, water `0.14` | Weights albedo, emissivity, storage heat, evaporation, and sensible heat. | Heat storage and evaporation reflect the sample surface mix, not the target place. |
| Weather forcing | `Kc_2012_data_60.txt` | Supplies radiation, air temperature, humidity, wind, and rain. | The result describes the sample weather year, not the hackathon city period. |

## Diagnostic caveat

The diagnostic report found no fatal failures, but it kept one warning:

`Mean closure residual 5.731 exceeds 0.10.`

For this setup task, that does not stop the smoke test: the run completed, output
exists, provenance exists, and QH/QE/QN had 0.0% missing values. For the real
hackathon, this kind of warning should be explained in the public write-up and
followed up with the SUEWS table leads if it appears in the real city run.

## How to use this lesson in the hackathon

The winning move is not just "make SUEWS run." The stronger move is to show:

1. What question you asked.
2. What you changed from the template.
3. What you deliberately left as an assumption.
4. Why those choices matter physically.
5. What the result can support, and what it cannot support.

Priority order for replacing sample assumptions:

1. Location and timezone.
2. Weather forcing.
3. Land-cover fractions and albedo.
4. Anthropogenic heat drivers.
5. Material and thermal properties.
6. Vegetation and water assumptions.

In the public Pages story, include a short "adjusted vs still assumed" table.
That honesty is part of doing well, not a weakness.
