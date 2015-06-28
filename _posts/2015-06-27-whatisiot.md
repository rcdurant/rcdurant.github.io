---
layout: page
title: What is iot?
category: faq
date: '2015-06-27 16:04'
order: 1
---

#What is iot?
**iot** is a Linux application program that inserts the I/O toolkit middleware into the environment of all child processes of iot. iot has several options that allow for customizable instrumentation.

Wild card name selection of programs and files affected by iot middleware
Each child of iot generates its own ilz stream
Optional merging of all generated ilz streams into a single stream
Collection of kernel instrumentation such as diskstats, netstats, meminfo, and cpustat
Optional delay of iot intervention in programs until `MPI_Initialized()` returns true.
###Benefits

- No root permission needed
- No recompiling or relinking
- Minimal changes to run scripts
- Compatible with MPI
- Low overhead

###Examples
iot command is a pre-command, such as time:

```
% iot -f dd.icf dd if=/dev/zero of=/dev/null count=1024 bs=1m
```

iot arguments

```
​-f <icf_file_name>
​-c <file> collect all iol results in file
​​-m delay iot interception until MPI_Initialized() returns true
```

Processes downstream of the iot process are selectable for instrumentation, based on the pathname of the program being executed, by directives in an iot configuration file (icf):
```
PROGRAMS.include={*.exe:a.out}.exclude={sh:csh}
```

icf example

```
​ilz.name={${PROGRAM}.${PID}}.directory={${HOME}/ilz}
​​diskstats.interval={500}.devices={sd*}
​​meminfo.interval={500}
​​PROGRAMS.include={*.exe}.exclude{/bin/*}
​​​   FILES.include={/tmp/**}
​​​​      LAYERS.use={trc,psx}
```
