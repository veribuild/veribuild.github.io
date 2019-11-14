---
layout: default
title: compare
---

This page contains the comparison results of VeriBuild and MkCheck.

## Tips

- To compare with MkCheck, which reports missing dependency edges instead of targets, we convert the results of VeriBuild to the file-level records used by MkCheck for comparison.
- In the projects, including OpenCV, Python, and PHP, MkCheck reports an overwhelmingly amount of missing dep edges (no. of targets X no. of files). We omit the reports for these projects.
- MkCheck fails to analyze LLVm and OpenSSL; there are no comparison results for these two projects.
- The second column indicates the number of MDs reported by MkCheck, MDs reported VeriBuild, and MDs that both tools report. The third column indicates the detailed info of RD. The fourth column is the remark indicating the conclusion of the comparison.

## Details of Results

| Project Name | MD(M,V,shared) | RD(M,V,shared) | Remark |
| :----------- | :---------- | :--------------- | :------------ |
| [fastText](compare/fastText.json) | [0, 10, 0] | [0, 0, 0] | Equivalent |
| [8cc](compare/8cc.json) | [0, 0, 0] | [0, 0, 0]| Identical |
| [Generic-C-Project](compare/Generic-C-Project.json) | [0, 0, 1] | [0, 0, 0] | Identical |
| [neven](compare/neven.json) | [0, 0, 1649] | [0, 0, 0] | Identical |
| [cctz](compare/cctz.json) | [0, 0, 0] | [0, 0, 0] | Identical |
| [mpc](compare/mpc.json) | [0, 22, 0] | [146, 0, 0] | VeriBuild>MkCheck |
| [tig](compare/tig.json) | [0, 0, 0] | [0, 0, 0]| Identical |
| [x86-thing](compare/x86-thing.json) | [0, 0, 76] | [1, 0, 0] | Equivalent |
| [gwion-util](compare/gwion-util.json) | [0, 0, 0] | [0, 0, 8] | Identical |
| [namespaced_parser](compare/namespaced_parser.json) | [1, 2, 5] | [0, 0, 0] | Equivalent |
| [lec](compare/lec.json) | [0, 0, 2] | [0, 0, 0] | Identical |
| [Bftpd](compare/bftpd.json) | [0, 0, 9] | [97, 0, 0] | Equivalent |
| [grbl](compare/grbl.json) | [0, 0, 22] | [0, 0, 0] | Identical |
| [cJSON](compare/cJSON.json) | [0, 0, 1] | [0, 0, 0] | Identical |
| [gravity](compare/gravity.json) | [0, 262, 0] | [4, 0, 0] | VeriBuild>MkCheck |
| [LAME](compare/lame-3.100.json) | [63, 25165, 3] | [324, 0, 0] | Different |
| [Capstone](compare/capstone.json) | [5854, 4652, 123] | [1231, 207, 0] | VeriBuild>MkCheck |
| [libco](compare/libco.json) | [40, 3, 31] | [20, 0, 0] | VeriBuild>MkCheck |
| [Bash](compare/bash-5.0.json) | [318, 9623, 1511] | [617, 45, 0]| VeriBuild>MkCheck |
| [greatest](compare/greatest.json) | [0, 0, 1] | [0, 0, 0] | Identical |
| [GNU Aspell](compare/aspell.json) | [103, 55, 0] | [1617, 0, 0] | VeriBuild>MkCheck |
| [Redis](compare/redis.json) | [5, 6414, 349] | [5, 0, 0] | VeriBuild>MkCheck |
| [ck](compare/ck.json)  | [0, 0, 216] | [37011, 0, 0] | Equivalent |
| [zlib](compare/zlib.json) | [0, 0, 3] | [0, 0, 0] | Identical |
| [lighttpd](compare/lighttpd-1.4.53.json) | [104, 69785, 0] | [707, 4, 0] | Different |
| [Tmux](compare/tmux.json) | [0, 1, 0] | [0, 0, 0]| Equivalent |
| [fzy](compare/fzy.json) | [0, 0, 17] | [1, 0, 0] | Equivalent |
| [Stack-RNN](compare/Stack-RNN.json) | [0, 14, 0] | [4, 0, 0] | VeriBuild>MkCheck |
| [CacheSimulator](compare/CacheSimulator.json) | [0, 1, 2] | [0, 0, 0]| Equivalent |
| [kleaver](compare/kleaver.json) | [2, 11, 0] | [0, 0, 0] | Equivalent |
| [http-parser](compare/http-parser.json) | [0, 0, 0] | [0, 0, 0] | Identical |
| [clib](compare/clib.json) |[0, 31, 147] | [6, 0, 0]| Different |
| [Cppcheck](compare/cppcheck-1.87.json) | [0, 16, 0] | [21, 0, 0]| VeriBuild>MkCheck |

## Some Explanations

The labels in the Remark column include:

- Identical: The bug reports of MkCheck and VeriBuild are the same.
- Equivalent: Even though their reports are not identical at the dependency edge level, however, when mapped to the target-level, their reports are the same.
- Different: The reports are different for MkCheck and VeriBuild.
- VeriBuild>MkCheck: MkCheck intentionally skips some files in its implementation. Our approach has no such compromise, which results in more reports than MkCheck.
