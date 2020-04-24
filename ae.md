---
layout: default
title: Artifact Evaluation Tutorial
---

This page contains the comparison results of VeriBuild and MkCheck.

## The Jenkins System

With the login information attached in the email, you can login a Jenkins system for running different veribuild tasks. 
![First Page of the Jenkins System](/assets/images/jenkins-frontpage.jpg)

| Project Name | Content |
| :----------- | :---------- |
| vemake_buildfuzz_a_project | Run Build Fuzzing for a project |
| vemake_run_veribuild_for_one_project | Run Veribuild MP or RD check for a project |
| vemake_run_FR| Run Veribuild FR check for a project |

## The source code of Veribuild

With the login provided in the review package. You can find the source code of Veribuild in:

```bash
/home/vemakecreator/CODEBASE/veribuild/Vemake/VemakeTool/vemake/tool
```

The source code will be open sourced after the review process and rewriting documents. 


## How to run BuildFuzzing job


1. Click vemake_buildfuzz_a_project . 
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


6. To inspect the source code of the script used for running this job, click "Configure". 
You can find the script code in the "Build" Section. 



## How to run a Veribuild job

Similar to running a BuildFuzzing job. Click the "vemake_run_veribuild_for_one_project". 

There are three parameters for this job. 

| Parameter Name | Content |
| :----------- | :---------- |
| PROJECTS | Select the project to be checked with Veribuild |
| RULES | MP = Missing Dependency  EP = Redundant/Excessive Dependency |
| NO_CACHE| NO_CACHE=True  => Do not use cache during the analysis |


We use a project **CacheSimulator** to illustrate how to run Veribuild on it. 

1. Click the Task "vemake_run_veribuild_for_one_project". 
2. Click "Build With Parameters"
3. Select CacheSimulator in the PROJECT section, 
   "EP, MP" in the Rules section. 
   Leave the checkbox unchecked in the "NO_CACHE" section (to reuse build cache).
  
![Veribuild Config](/assets/images/veribuild_config.jpg)

4. Click the build button. 
5. Click the new job appeared in the build history section. 
6. Click "Console output" to view the output of running Veribuild. 

Here is an example:
### Check results:

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



