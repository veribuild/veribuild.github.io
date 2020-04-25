---
layout: default
title: Artifact Evaluation Tutorial
---
## Terms

- RD/EP: RD=Redundant Dependency, EP=Excessive Prerequisite. They are two names of the same kind of issues. 
- MD/MP: MD=Missing Dependency, MP=Missing Prerequisite. They are two names of the same kind of issues. 
- FR: File Race

## The Jenkins System

With the login information attached in README, you can login a Jenkins system for running different Veribuild tasks. 
![First Page of the Jenkins System](/assets/images/jenkins-frontpage.jpg)

| Project Name | Content |
| :----------- | :---------- |
| vemake_buildfuzz_a_project | Run Build Fuzzing for a project |
| vemake_run_veribuild_for_one_project | Run Veribuild MP or RD check for a project |
| vemake_run_FR| Run Veribuild FR check for a project |

## The source code of Veribuild

With the login information provided in README, you can find the source code of Veribuild in:

```bash
/home/vemakecreator/CODEBASE/veribuild/Vemake/VemakeTool/vemake/tool
```

The source code will be open-sourced after the review process and rewriting documents. 


## How to run BuildFuzzing job


1. Click **vemake_buildfuzz_a_project**. 
2. Click "Build with Parameters" to start a job. 
    - In the build parameter section, select a project for testing (e.g., CacheSimulator). 
3. Click Build to trigger this job
![Build Fuzzing Task](/assets/images/fuzz_task.png)

4. To inspect the console output, click the job in the "Build History Column". 
![Build Fuzzing Job](/assets/images/fuzz_runningjob.png)

5. To view the result of Build Fuzzing, go back to the project page and check its artifacts:

![Build Fuzzing Workspace](/assets/images/fuzz_workspace.png)

Here is an example of the output of build fuzzing:

```bash
[1/7] /home/nand/Vemake/testbase/testproject/CacheSimulator/cachelab.c:
[2/7] /home/nand/Vemake/testbase/testproject/CacheSimulator/cachelab.h:
  - /home/nand/Vemake/testbase/testproject/CacheSimulator/trans.o (x86_64-linux-gnu-as)
[3/7] /home/nand/Vemake/testbase/testproject/CacheSimulator/contracts.h:
  - /home/nand/Vemake/testbase/testproject/CacheSimulator/trans.o (x86_64-linux-gnu-as)
[4/7] /home/nand/Vemake/testbase/testproject/CacheSimulator/csim.c:
[5/7] /home/nand/Vemake/testbase/testproject/CacheSimulator/test-trans.c:
[6/7] /home/nand/Vemake/testbase/testproject/CacheSimulator/tracegen.c:
[7/7] /home/nand/Vemake/testbase/testproject/CacheSimulator/trans.c:
```

This example shows two missing dependencies: **trans.o -> cachelab.h**,  and **trans.o->contracts.h**. 

{:start="6"}
6. To inspect the source code of the script used for running this job, click "Configure". 
You can find the script code in the "Build" section. 



## How to run a Veribuild job

Similar to running a BuildFuzzing job. Click the "vemake_run_veribuild_for_one_project". 

There are three parameters for this job. 

| Parameter Name | Content |
| :----------- | :---------- |
| PROJECTS | Select the project to be checked with Veribuild |
| RULES | MP = Missing Dependency <br /> EP = Redundant/Excessive Dependency |
| NO_CACHE| NO_CACHE=True  <br /> => Do not use cache during the analysis |


We use a project **CacheSimulator** to illustrate how to run Veribuild on it. 

1. Click the Task "vemake_run_veribuild_for_one_project". 
2. Click "Build With Parameters"
3. Select CacheSimulator in the PROJECT section, 
   "EP, MP" in the Rules section. 
   Leave the checkbox unchecked in the "NO_CACHE" section (to reuse build cache).
  
![Veribuild Config](/assets/images/veribuild_config.jpg)

{:start="4"}
4. Click the build button. 
5. Click the new job that appeared in the build history section. 
6. Click "Console output" to view the output of running Veribuild. 

Here is an example:
### Check results

In the "Console output", you can find a section in the log similar to :

```bash
===== Start Detecting Missing Dependencies:
Missing Dependency Detected : trans.o -> /home/vemakecreator/Vemake/testbase/testproject/CacheSimulator/cachelab.h
Missing Dependency Detected : trans.o -> /home/vemakecreator/Vemake/testbase/testproject/CacheSimulator/contracts.h
Missing Dependency Detected : tracegen -> /home/vemakecreator/Vemake/testbase/testproject/CacheSimulator/cachelab.h
===== Finish Missing Dependency Detection with success
MP detection finished
===== Start Detecting Excessive/Redundant Dependencies:
===== Finish Excessive/Redundant Dependency Detection with Success
EP detection finished
``` 

For this project we have detected two MP issues reported the paper: 

- **trans.o** -> **cachelab.h**, **contracts.h** 
- **tracegen** -> **cachelab.h**

Note: two missing edges for the same target are counted as one MP issue. 

For more results, we have prepared a more reviewer-friendly page, please check the [online bug reporting system page](/list): 



## Report filtering 

When evaluating Redundant Dependency Detection, we apply a set of filters to the results. 
Here is the filter code in Python:

```bash
    
# A set with all non-makefile edges filtered.
mc_ep_set_with_non_make_edges = set([(s,t) for s,t in mc_ep_set if SDG.has_node(s) and SDG.has_node(t)])
results["n_mc_mfile"] = len(mc_ep_set_with_non_make_edges)

# Ignore Config Edges. 
config_files = ["config.h", "settings.h", "config.h.in"]
mc_config_ep = set(filter(lambda t: "config" in t[1] or "setting" in t[1], mc_ep_set_with_non_make_edges))
results["n_mc_conf"] = len(mc_config_ep)
mc_ep_set_with_non_make_edges = mc_ep_set_with_non_make_edges - mc_config_ep

vb_config_ep = set(filter(lambda t: "config" in t[1] or "setting" in t[1], vb_ep_set))
results["n_vb_conf"] = len(vb_config_ep)
vb_ep_set = vb_ep_set - vb_config_ep

```

For more details, please refer to the source code at this path:
```bash
/home/vemakecreator/CODEBASE/veribuild/Vemake/VemakeTool/vemake/tool/src/Validator/ep_comparator.py
```

[comment]: # (## Some Explanations)

## Run Veribuild on a New Project

We will use a test project **hashcat** to illustrate how to test Veribuild on a new project. 
[Hashcat:https://github.com/hashcat/hashcat](https://github.com/hashcat/hashcat)

1. Login the server provided in README. 

2. Download and build the project. Make sure it can be compiled correctly. 
   
```bash
vemakecreator@4be2198f6def:~$ cd test_new_project/
vemakecreator@4be2198f6def:~/test_new_project$ git clone https://github.com/hashcat/hashcat.git
vemakecreator@4be2198f6def:~/test_new_project$ cd hashcat/
vemakecreator@4be2198f6def:~/test_new_project/hashcat$ make -j80
vemakecreator@4be2198f6def:~/test_new_project/hashcat$ make clean
```

{:start="3"}
3. Run Veribuild Manually:

```bash
(cd /home/vemakecreator/CODEBASE/veribuild/Vemake/VemakeTool/vemake/tool/src && /home/vemakecreator/CODEBASE/veribuild/Vemake/VemakeTool/vemake/tool/src/run.py -f /home/vemakecreator/test_new_project/hashcat -EP -MP)
```

- -f is used to specify the project dir, which contains a Makefile.
- -MP to enable detection of Missing Dependencies. 
- -EP to enable detection of Redundant Dependencies.

After executing, you can inspecting the results from console output, for example:

```bash
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/xxHash/bits/stdlib.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/include/alloca.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/xxHash/bits/stat.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/include/bits/wordsize.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/LZMA-SDK/C/bits/posix1_lim.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/include/time.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/include/bits/fcntl-linux.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/xxHash/bits/string2.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/zlib/bits/stdio.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/xxHash/bits/endian.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/include/stdarg.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/include/bits/huge_val.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/xxHash/gnu/stubs.h
Missing Dependency Detected : modules/module_12900.so -> /home/vemakecreator/test_new_project/hashcat/deps/OpenCL-Headers/emmintrin.h
===== Finish Missing Dependency Detection with success
MP detection finished
===== Start Detecting Excessive/Redundant Dependencies:
Excessive Dependency Detected : install_docs -> install_make_shared_root
Excessive Dependency Detected : distclean -> clean
Excessive Dependency Detected : install_shared -> install_make_shared_root
Excessive Dependency Detected : install_library_dev -> install_make_library_dev_root
===== Finish Excessive/Redundant Dependency Detection with Success
EP detection finished
pre_time   358.99005365371704
CDG time   15.144007921218872
DDG time   323.52200055122375
res time   20.324045181274414
MP_time    18.13148856163025
EP_time    0.11908316612243652
FT_time    0
FR_time    0
/home/vemakecreator/test_new_project/hashcat test finished
```  

You can see from the output that we can detect many missing dependencies in this project. 
Those redundant dependencies are False Positive reports, as we have discussed in the paper (Page 8). 

```bash
Another category of false RDs are order-only prerequisites. Developers
specify the build rules to enforce the build order of different
targets. instead of the input-output dependencies. For example, in
Figure 8, at line 946 in Makefile.in, the developer specifies force
as the dependency of test, tests and check. The build of the three
targets does not rely on any output from building force, but the
developer intends to build them only after the build of force. To be
more efficient, one can specify such dependencies as order-only
prerequisites[10] supported by Make, and VeriBuild can utilize
this information to filter out false RDs caused by order-only prerequisites.
```


And you can also find the JSON-formatted results (MP.json and EP.json) at the this path:

```bash
/home/vemakecreator/CODEBASE/veribuild/Vemake/testbase/testoutput/hashcat
```

