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

## SUEWS citation

This repository should cite SUEWS in any real submission:

- Jarvi, L., Grimmond, C.S.B. and Christen, A. (2011). The Surface Urban Energy
  and Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver.
  Journal of Hydrology, 411(3-4), 219-237.
- Ward, H.C., Kotthaus, S., Jarvi, L. and Grimmond, C.S.B. (2016). Surface Urban
  Energy and Water Balance Scheme (SUEWS): Development and evaluation at two UK
  sites. Urban Climate, 18, 1-32.
