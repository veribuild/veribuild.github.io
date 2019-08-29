---
layout: default
title: compare
---

This page contains the comparison results of VeriBuild and MkCheck.

## Tips
- We split the results of Veribuild from target-level to file-level, and tried to match the file-to-file edges with the reports of MkCheck.
- In the projects including OpenCV, Python and PHP, the report list of MkCheck are too long to  be compared with VeriBuild, so we omitted these reports in the following list.
- Due to the crashes of MkCheck, the comparison results of LLVM and OpenSSL are not listed.
- The second column indicates the number of MD reports only provided by MkCheck, MD reports only provided by Veribuild, and the MD reports both provided by these two tools(in `shared`). The third column indicates the detailed info of RD.

## Details of Results
| Project Name | MD(MkCheck,VeriBuild,shared) | RD(MkCheck,VeriBuild,shared) |
| :----------- | :---------- | :--------------- |
| [fastText](compare/fastText.json) | [0, 10, 0] | [0, 0, 0] |
| [8cc](compare/8cc.json) | [0, 0, 0] | [0, 0, 0]|
| [Generic-C-Project](compare/Generic-C-Project.json) | [0, 0, 1] | [0, 0, 0] |
| [neven](compare/neven.json) | [0, 0, 1649] | [0, 0, 0] |
| [cctz](compare/cctz.json) | [0, 0, 0] | [0, 0, 0] |
| [mpc](compare/mpc.json) | [0, 22, 0] | [146, 0, 0] |
| [tig](compare/tig.json) | [0, 0, 0] | [0, 0, 0]|
| [x86-thing](compare/x86-thing.json) | [0, 0, 76] | [1, 0, 0] |
| [gwion-util](compare/gwion-util.json) | [0, 0, 0] | [0, 0, 8] |
| [namespaced_parser](compare/namespaced_parser.json) | [1, 2, 5] | [0, 0, 0] |
| [lec](compare/lec.json) | [0, 0, 2] | [0, 0, 0] |
| [Bftpd](compare/bftpd.json) | [0, 0, 9] | [97, 0, 0] |
| [grbl](compare/grbl.json) | [0, 0, 22] | [0, 0, 0] |
| [cJSON](compare/cJSON.json) | [0, 0, 1] | [0, 0, 0] |
| [gravity](compare/gravity.json) | [0, 262, 0] | [4, 0, 0] |
| [LAME](compare/lame-3.100.json) | [63, 25165, 3] | [324, 0, 0] |
| [Capstone](compare/capstone.json) | [5854, 4652, 123] | [1231, 207, 0] |
| [libco](compare/libco.json) | [40, 3, 31] | [20, 0, 0] |
| [Bash](compare/bash-5.0.json) | [318, 9623, 1511] | [617, 45, 0]|
| [greatest](compare/greatest.json) | [0, 0, 1] | [0, 0, 0] |
| [GNU Aspell](compare/aspell.json) | [103, 55, 0] | [1617, 0, 0] |
| [Redis](compare/redis.json) | [5, 6414, 349] | [5, 0, 0] |
| [ck](compare/ck.json)  | [0, 0, 216] | [37011, 0, 0] |
| [zlib](compare/zlib.json) | [0, 0, 3] | [0, 0, 0] |
| [lighttpd](compare/lighttpd-1.4.53.json) | [104, 69785, 0] | [707, 4, 0] |
| [Tmux](compare/tmux.json) | [0, 1, 0] | [0, 0, 0]|
| [fzy](compare/fzy.json) | [0, 0, 17] | [1, 0, 0] |
| [Stack-RNN](compare/Stack-RNN.json) | [0, 14, 0] | [4, 0, 0] |
| [CacheSimulator](compare/CacheSimulator.json) | [0, 1, 2] | [0, 0, 0]|
| [kleaver](compare/kleaver.json) | [2, 11, 0] | [0, 0, 0] |
| [http-parser](compare/http-parser.json) | [0, 0, 0] | [0, 0, 0] |
| [clib](compare/clib.json) |[0, 31, 147] | [6, 0, 0]|
| [Cppcheck](compare/cppcheck-1.87.json) | [0, 16, 0] | [21, 0, 0]|

