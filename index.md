---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: VeriBuild
---

## News
- Fix 1 missing dependency in [cJSON](https://github.com/DaveGamble/cJSON/pull/380) has been confirmed. The number of confirmed dependency error has reached 411(Update on Step 11, 2019)
- Fix 12 missing dependencies in [MPC](https://github.com/orangeduck/mpc/pull/115) have been confirmed. The number of confirmed dependency errors has reached 410. (Update on Step 2, 2019)
- 398 dependency errors have been confirmed. (Update on Aug 24, 2019)

## Tips for YOU
There are some necessary tips for you, which can help you to understand the reports.
- VeriBuild is a general approach for dependency error detection and Vemake is an instance of VeriBuild customized for GNU Make. The reports of VeriBuild were submitted by the github account [vemakereporter](https://github.com/vemakereporter) or SourceForge account.
- In the report lists of VeriBuild published in Effectiveness part, MP(Missing Prerequisite) means MD(Missing Dependency), and EP(Excessive Prerequisite) means RD(Redundant Dependency).

## Effectiveness
If you want to know the details of the reports provided by Veribuild, you can read this [list](/list).

## Efficiency
If you want to know the comparison results of VeriBuild and MkCheck, you can read this [list](/compare).