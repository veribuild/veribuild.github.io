---
layout: default
title: compare
---

This page contains the comparison results of VeriBuild and MkCheck.

## Tips

- We split the results of VeriBuild from target-level to file-level, and tried to match the file-to-file edges with the reports of MkCheck.
- In the projects including OpenCV, Python and PHP, the report list of MkCheck are too long to  be compared with VeriBuild, so we omitted these reports in the following list.
- Due to the crashes of MkCheck, the comparison results of LLVM and OpenSSL are not listed.
- The second column indicates the number of MD reports only provided by MkCheck, MD reports only provided by VeriBuild, and the MD reports both provided by these two tools(in `shared`). The third column indicates the detailed info of RD. The fourth column is the remark indicating the conclusion of the comparison.

## Details of Results

| Project Name | MD(M,V,shared) | RD(M,V,shared) | Remark |
| :----------- | :---------- | :--------------- | :------------ |
| [fastText](compare/fastText.json) | [0, 10, 0] | [0, 0, 0] | Equivalence |
| [8cc](compare/8cc.json) | [0, 0, 0] | [0, 0, 0]| Totally Same |
| [Generic-C-Project](compare/Generic-C-Project.json) | [0, 0, 1] | [0, 0, 0] | Totally Same |
| [neven](compare/neven.json) | [0, 0, 1649] | [0, 0, 0] | Totally Same |
| [cctz](compare/cctz.json) | [0, 0, 0] | [0, 0, 0] | Totally Same |
| [mpc](compare/mpc.json) | [0, 22, 0] | [146, 0, 0] | Reasonable Difference |
| [tig](compare/tig.json) | [0, 0, 0] | [0, 0, 0]| Totally Same |
| [x86-thing](compare/x86-thing.json) | [0, 0, 76] | [1, 0, 0] | Equivalence |
| [gwion-util](compare/gwion-util.json) | [0, 0, 0] | [0, 0, 8] | Totally Same |
| [namespaced_parser](compare/namespaced_parser.json) | [1, 2, 5] | [0, 0, 0] | Equivalence |
| [lec](compare/lec.json) | [0, 0, 2] | [0, 0, 0] | Totally Same |
| [Bftpd](compare/bftpd.json) | [0, 0, 9] | [97, 0, 0] | Equivalence |
| [grbl](compare/grbl.json) | [0, 0, 22] | [0, 0, 0] | Totally Same |
| [cJSON](compare/cJSON.json) | [0, 0, 1] | [0, 0, 0] | Totally Same |
| [gravity](compare/gravity.json) | [0, 262, 0] | [4, 0, 0] | Reasonable Difference |
| [LAME](compare/lame-3.100.json) | [63, 25165, 3] | [324, 0, 0] | Others |
| [Capstone](compare/capstone.json) | [5854, 4652, 123] | [1231, 207, 0] | Reasonable Difference |
| [libco](compare/libco.json) | [40, 3, 31] | [20, 0, 0] | Reasonable Difference |
| [Bash](compare/bash-5.0.json) | [318, 9623, 1511] | [617, 45, 0]| Reasonable Difference |
| [greatest](compare/greatest.json) | [0, 0, 1] | [0, 0, 0] | Totally Same |
| [GNU Aspell](compare/aspell.json) | [103, 55, 0] | [1617, 0, 0] | Reasonable Difference |
| [Redis](compare/redis.json) | [5, 6414, 349] | [5, 0, 0] | Reasonable Difference |
| [ck](compare/ck.json)  | [0, 0, 216] | [37011, 0, 0] | Equivalence |
| [zlib](compare/zlib.json) | [0, 0, 3] | [0, 0, 0] | Totally Same |
| [lighttpd](compare/lighttpd-1.4.53.json) | [104, 69785, 0] | [707, 4, 0] | Others |
| [Tmux](compare/tmux.json) | [0, 1, 0] | [0, 0, 0]| Equivalence |
| [fzy](compare/fzy.json) | [0, 0, 17] | [1, 0, 0] | Equivalence |
| [Stack-RNN](compare/Stack-RNN.json) | [0, 14, 0] | [4, 0, 0] | Reasonable Difference |
| [CacheSimulator](compare/CacheSimulator.json) | [0, 1, 2] | [0, 0, 0]| Equivalence |
| [kleaver](compare/kleaver.json) | [2, 11, 0] | [0, 0, 0] | Equivalence |
| [http-parser](compare/http-parser.json) | [0, 0, 0] | [0, 0, 0] | Totally Same |
| [clib](compare/clib.json) |[0, 31, 147] | [6, 0, 0]| High Similarity |
| [Cppcheck](compare/cppcheck-1.87.json) | [0, 16, 0] | [21, 0, 0]| Reasonable Difference |

## Some Explanations

The labels in the Remark column include:

- Totally Same: The bug reports of MkCheck and VeriBuild are the same.
- Equivalence: MkCheck and VeriBuild detect the dependency errors in the file-level and the target-level respectively, so MkCheck tends to report much more RD reports and VeriBuild can provide some reports relevant to non-file target, which MkCheck can not provide. They share other MD and RD reports regardless of these differences.
- High Similarity: Most of the reports are shared by MkCheck and VeriBuild.
- Reasonable Difference: In these project, MkCheck only performs fuzz testing on the files it's interested in, which cannot report the bugs detected by VeriBuild, especially the MD reports. Almost all of these reports have been confirmed by the developers, which demonstrate the accuracy of VeriBuild. These cases are caused by the strategy of fuzzing configured in MkCheck.
- Others: Due to the level of the detections, we need to convert the reports of VerBuild from target-level to file-level. This process might cause the precision loss. 