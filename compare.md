---
layout: default
title: compare
---

This page contains the comparison results of VeriBuild and MkCheck.

## Tips

- To compare with MkCheck, which reports missing dependency edges instead of targets, we convert the results of VeriBuild to the file-level records used by MkCheck for comparison.
- In the projects, including OpenCV, Python, and PHP, MkCheck reports an overwhelmingly amount of missing dep edges (no. of targets X no. of files). We omit the reports for these projects.
- MkCheck fails to analyze LLVM and OpenSSL; there are no comparison results for these two projects.
- The second column indicates the number of MDs reported by MkCheck, MDs reported VeriBuild, and MDs that both tools report. The third column indicates the detailed info of RD. The fourth column is the remark indicating the conclusion of the comparison.

## Details of Results

| Project Name | MD(M,V,shared) | RD(M,V,shared) | Remark |
| :----------- | :---------- | :--------------- | :------------ |
| [fastText](compare/fastText.json) | [0, 10, 0] | [0, 0, 0] | VeriBuild>MkCheck                                            |
| [8cc](compare/8cc.json) | [0, 0, 0] | [0, 0, 0]| VeriBuild=MkCheck |
| [Generic-C-Project](compare/Generic-C-Project.json) | [0, 0, 1] | [0, 0, 0] | VeriBuild=MkCheck |
| [neven](compare/neven.json) | [0, 0, 1649] | [0, 0, 0] | VeriBuild=MkCheck |
| [cctz](compare/cctz.json) | [0, 0, 0] | [0, 0, 0] | VeriBuild=MkCheck |
| [mpc](compare/mpc.json) | [0, 22, 0] | [146, 0, 0] | TO BE CHECKED(Attention) |
| [tig](compare/tig.json) | [0, 0, 0] | [0, 0, 0]| VeriBuild=MkCheck |
| [x86-thing](compare/x86-thing.json) | [0, 0, 76] | [1, 0, 0] | TO BE CHECKED(VeriBuild $\geq$ MkCheck)                      |
| [gwion-util](compare/gwion-util.json) | [0, 0, 0] | [0, 0, 8] | VeriBuild=MkCheck |
| [namespaced_parser](compare/namespaced_parser.json) | [1, 2, 5] | [0, 0, 0] | TO BE CHECKED(VeriBuild=MkCheck)                             |
| [lec](compare/lec.json) | [0, 0, 2] | [0, 0, 0] | VeriBuild=MkCheck |
| [Bftpd](compare/bftpd.json) | [0, 0, 9] | [97, 0, 0] | TO BE CHECKED(Attention) |
| [grbl](compare/grbl.json) | [0, 0, 22] | [0, 0, 0] | VeriBuild=MkCheck |
| [cJSON](compare/cJSON.json) | [0, 0, 1] | [0, 0, 0] | VeriBuild=MkCheck |
| [gravity](compare/gravity.json) | [0, 262, 0] | [4, 0, 0] | VeriBuild>MkCheck |
| [LAME](compare/lame-3.100.json) | [63, 25165, 3] | [324, 0, 0] | TO BE CHECKED(Attention) |
| [Capstone](compare/capstone.json) | [5854, 4652, 123] | [1231, 207, 0] | TO BE CHECKED(Attention) |
| [libco](compare/libco.json) | [40, 3, 31] | [20, 0, 0] | TO BE CHECKED(Attention) |
| [Bash](compare/bash-5.0.json) | [318, 9623, 1511] | [617, 45, 0] | TO BE CHECKED(Attention)                                     |
| [greatest](compare/greatest.json) | [0, 0, 1] | [0, 0, 0] | VeriBuild=MkCheck |
| [GNU Aspell](compare/aspell.json) | [103, 55, 0] | [1617, 0, 0] | TO BE CHECKED(Attention) |
| [Redis](compare/redis.json) | [5, 6414, 349] | [5, 0, 0] | TO BE CHECKED(Attention) |
| [ck](compare/ck.json)  | [0, 0, 216] | [37011, 0, 0] | VeriBuild=MkCheck(Remark) |
| [zlib](compare/zlib.json) | [0, 0, 3] | [0, 0, 0] | VeriBuild=MkCheck |
| [lighttpd](compare/lighttpd-1.4.53.json) | [104, 69785, 0] | [707, 4, 0] | TO BE CHECKED(Attention) |
| [Tmux](compare/tmux.json) | [0, 1, 0] | [0, 0, 0]| VeriBuild>MkCheck |
| [fzy](compare/fzy.json) | [0, 0, 17] | [1, 0, 0] | TO BE CHECKED(VeriBuild>MkCheck, FP in MkCheck) |
| [Stack-RNN](compare/Stack-RNN.json) | [0, 14, 0] | [4, 0, 0] | VeriBuild>MkCheck |
| [CacheSimulator](compare/CacheSimulator.json) | [0, 1, 2] | [0, 0, 0]| VeriBuild>MkCheck |
| [kleaver](compare/kleaver.json) | [2, 11, 0] | [0, 0, 0] | VeriBuild>MkCheck(Remark: binary target is not easy comprehensive) |
| [http-parser](compare/http-parser.json) | [0, 0, 0] | [0, 0, 0] | VeriBuild=MkCheck |
| [clib](compare/clib.json) |[0, 31, 147] | [6, 0, 0]| VeriBuild<MkCheck(Attention) |
| [Cppcheck](compare/cppcheck-1.87.json) | [0, 16, 0] | [21, 0, 0]| TO BE CHECK(Attention)                                       |

## Some Explanations

The labels in the Remark column include:

- Identical: The bug reports of MkCheck and VeriBuild are the same.
- Equivalent: Even though their reports are not identical at the dependency edge level, however, when mapped to the target-level, their reports are the same.
- Different: The reports are different for MkCheck and VeriBuild.
- VeriBuild>MkCheck: MkCheck intentionally skips some files in its implementation. Our approach has no such compromise, which results in more reports than MkCheck.
