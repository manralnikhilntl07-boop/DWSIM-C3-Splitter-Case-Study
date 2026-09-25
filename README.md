# DWSIM-C3-Splitter-Case-Study
Chevron-inspired DWSIM simulation for polymer-grade propylene production using a 100 kmol/h, 70/30 propylene–propane feed and Peng–Robinson thermodynamics. A two-column system achieved 99.98% propylene purity, 96.05% propane purity, with 3.98 MW potential internal heat recovery.

# Chevron-Inspired C3 Splitter --- DWSIM Case Study

## Overview

This project develops a two-column DWSIM simulation for the separation
of a propylene/propane (C3) mixture into a high-purity propylene product
and a recovered propane-rich product.

The architecture is **Chevron-inspired**, based on the published Port
Arthur C3 splitter benchmark, but it is **not a replica of Chevron's
proprietary process model**.

## Design basis

-   Fresh feed: **100 kmol/h**
-   Feed composition: **70 mol% C3H6 / 30 mol% C3H8**
-   Feed temperature: **298.15 K**
-   Thermodynamic model: **Peng--Robinson**
-   Main product: **polymer-grade propylene**
-   Final architecture: **2 distillation columns + energy integration**

## Industrial benchmark

The published Chevron Port Arthur benchmark reports:

-   2 series-operated C3 splitter towers
-   70 mol% propylene / 30 mol% propane feed
-   99.6 mol% propylene target purity
-   98.6% propylene recovery target
-   96.6 mol% propane target in the bottom product
-   214 theoretical stages used to represent the industrial tray system

Reference: Oil & Gas Journal, 6 Nov. 1995:
https://www.ogj.com/general-interest/companies/article/17216899/high-capacity-trays-debottleneck-texas-c3-splitter

## Final process structure

``` text
Fresh C3 Feed
     |
     v
+-----------+
|   C-101   |  Primary propylene splitter
+-----------+
   |      |
   |      +----------------------> Propylene-rich product
   |                               ~99.98 mol% C3H6
   v
+-----------+
|   C-102   |  Secondary recovery / propane-side separation
+-----------+
   |      |
   |      +----------------------> Propylene recovery
   |
   +-----------------------------> Recovered propane
```

An energy-recycle block couples the C-102 condenser with the C-101
reboiler.

## Latest simulation snapshot

  KPI                                                      Value
  -------------------------------------- -----------------------
  Propylene product purity                 **\~99.98 mol% C3H6**
  Propane-rich product purity              **\~96.05 mol% C3H8**
  C-101 condenser duty                               3,980.95 kW
  C-101 reboiler duty                                3,979.07 kW
  C-102 condenser duty                               6,159.55 kW
  C-102 reboiler duty                                6,160.85 kW
  Gross absolute column duty                          \~20.28 MW
  Potential C-101 reboiler heat offset                 \~3.98 MW
  Indicative duty-offset fraction                        \~19.6%

### Energy-integration note

The \~19.6% figure is a **simulation-level duty-offset calculation**,
not a final utility/economic saving. A rigorous heat-exchanger design
would require temperature approach, heat-transfer area, pressure drop
and utility-temperature checks.

## Recovery validation

Overall component recovery must be calculated using the final
system-boundary product streams:

**Propylene recovery**

`Recovery_C3H6 = C3H6 in final propylene product / 70 × 100`

**Propane recovery**

`Recovery_C3H8 = C3H8 in final propane product / 30 × 100`

The final saved DWSIM stream table should be used to populate these
values before publication.

## Why this is an engineering case study

The project demonstrates:

1.  Industrial process benchmarking
2.  Peng--Robinson thermodynamic modeling
3.  Shortcut distillation design
4.  Rigorous distillation simulation
5.  Reflux and feed-stage reasoning
6.  Two-column process architecture
7.  Product-purity targeting
8.  Component-recovery analysis
9.  Heat integration
10. Material and energy balance validation

## Key engineering lesson

Propylene/propane separation is difficult because the components have
very similar volatility. Conventional C3 splitters therefore require
high reflux and large stage counts. This makes energy integration an
important part of process design.

## Limitations

-   This is an educational/portfolio reconstruction, not a Chevron plant
    model.
-   DWSIM stage count alone does not establish hydraulic feasibility.
-   Heat integration requires temperature-driving-force verification.
-   Final overall recovery percentages should be taken from the
    reconciled final stream table.
-   No CAPEX or total annual cost claim is made.

## References

1.  Summers et al., *Oil & Gas Journal*, 1995 --- Chevron Port Arthur C3
    splitter benchmark.
2.  *Energy*, 2026 --- C3 splitter modeling/debottlenecking across
    pressure levels.
3.  *Chemical Engineering Research and Design* --- vapor recompression
    C3 splitter.
4.  *Energy*, 2006 --- internally heat-integrated propylene/propane
    splitter.
