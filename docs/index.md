# SUEWS hackathon practice setup

This page is a public practice page for the SUEWS Community Hackathon setup.
It is not the final judged hackathon analysis.

## Question

Can this repository run one small SUEWS example end to end using the
`suews-agent` tooling, and can the result be published with GitHub Pages?

## Practice run

I ran the bundled `simple-urban` starter case, which uses the KCL/London sample
configuration and forcing data. The run completed with SUEWS/SuPy `2026.6.5`
and wrote an hourly output file for 8,784 time steps.

The SUEWS agent checks used were `inspect_config`, `assess_readiness`,
`validate_config`, `diagnose_run`, and `summarise_run`.

Selected output summary:

| Variable | Mean | Min | Max | Missing |
| --- | ---: | ---: | ---: | ---: |
| QN | 44.76 | -83.80 | 646.98 | 0.0% |
| QH | 88.76 | -40.82 | 339.70 | 0.0% |
| QE | 27.58 | 1.70 | 195.34 | 0.0% |
| T2 | 11.91 | -5.24 | 30.40 | 0.0% |
| RH2 | 69.33 | 18.75 | 98.16 | 0.0% |

## Honest caveat

This is a setup check only. The site, land cover, and forcing come from the
bundled sample case, not the hackathon focus city. The diagnostic report found
no fatal failures, but it retained a warning about mean energy-balance closure
residual, so this result should not be used as scientific evidence.

## Sample assumptions still in this run

The SUEWS agent readiness check marked this as **Level 1 - demo**, not a
site-specific analysis. These inputs are still from the packaged sample case:

| Sample assumption | Current value | Why it matters |
| --- | --- | --- |
| Location | KCL/London, lat `51.51`, lon `-0.12`, altitude `10.7`, timezone `0.0` | This controls sun angle and radiation timing, which affects the energy balance. |
| Land cover | paved `0.43`, buildings `0.38`, evergreen trees `0.00`, deciduous trees `0.02`, grass `0.03`, bare soil `0.00`, water `0.14` | These fractions weight albedo, heat storage, evaporation, and sensible heat. |
| Weather forcing | `Kc_2012_data_60.txt` | This supplies radiation, air temperature, humidity, wind, and rain. |

## What this teaches for the hackathon

For the real hackathon city, the goal is not just to produce a number. A strong
submission should show what was changed from the template, what remained
assumed, and what that means for the heat-risk interpretation.

Most important inputs to replace or justify:

1. Location and timezone.
2. Weather forcing.
3. Land-cover fractions and albedo.
4. Anthropogenic heat drivers.
5. Material and thermal properties.
6. Vegetation and water assumptions.

The public story should include an "adjusted vs still assumed" table. Honest
caveats make the result more credible, not weaker.

## SUEWS citation

This repository should cite SUEWS in any real submission:

- Jarvi, L., Grimmond, C.S.B. and Christen, A. (2011). The Surface Urban Energy
  and Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver.
  Journal of Hydrology, 411(3-4), 219-237.
- Ward, H.C., Kotthaus, S., Jarvi, L. and Grimmond, C.S.B. (2016). Surface Urban
  Energy and Water Balance Scheme (SUEWS): Development and evaluation at two UK
  sites. Urban Climate, 18, 1-32.
