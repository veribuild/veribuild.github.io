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