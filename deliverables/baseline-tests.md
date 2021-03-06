---
layout: page
title: Data-Plane and Control-Plane Baseline Tests
---

The goal for this deliverable is for you to completete most (if not all) of the functionality required for both the data-plane and the control-plane. We expect that you will want to develop and test each of these planes independently from one another. After this deliverable (and before the interoperability test) you will work on integrating your data-plane and control-plane and making sure that all of your routers are interoperable. Do not underestimate the integration and interoperability aspects of this project, we expect that it will take at least a couple weeks to get right. That is why is it very important that you try to implement as much functionality as you can by the time this deliverable is due. To help get you started, we have provided some baseline data-plane and control-plane tests. These tests test *some* of the required functionality of your router so you will want to add more of your own. Please do not modify the provided baseline tests without instructor approval.

The baseline tests use the following test topology defined in [test_topology.py](https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18/blob/master/contrib-projects/sume-sdnet-switch/projects/simple_router/sw/simple_router_sw/simulation/test_topology.py).

```
               ##################
               eh0 - ip: 10.6.3.2
               ##################
                       |
                       |
                iface3:10.6.3.3   iface2:
             #################### 10.6.2.3        ##################
             self - rid: 10.6.0.3 --------------- r2 - rid: 10.2.0.3
             ####################        10.6.2.2 ##################
     iface1:10.6.1.3     iface0:10.6.0.3      10.2.0.3
            /                     \               /
           /                       \             /
     10.6.1.2                    10.6.0.2    10.2.0.2
##################                ##################
r1 - rid: 10.1.0.3                r0 - rid: 10.0.0.3
##################                ##################
       10.1.0.3                  10.0.0.3
           \                       /
            \                     /
           10.1.0.2          10.0.0.2
               ################## 10.3.1.3      #########################
               r3 - rid: 10.3.0.3 ------------- default route to internet
               ##################     0.0.0.0/0 #########################
                    10.3.0.3
                       |
                       |
                    10.3.0.2
              ################## 10.4.0.3        ########
              r4 - rid: 10.4.0.3 --------------- firewall
              ##################     10.4.0.0/16 ########
```

# Data-Plane Baseline Tests

The data-plane baseline tests are located in the simple_router's [gen_testdata.py](https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18/blob/master/contrib-projects/sume-sdnet-switch/projects/simple_router/testdata/gen_testdata.py#L167) script. Each test is defined by an input packet + metadata and an expected output packet + metadata. See the gen_testdata.py script for a short description of the functionality that each test is intended to exercise.

In order to run the tests, your `commands.txt` file should reflect the following topology:
```
               ##################
               eh0 - ip: 10.6.3.2
               ##################
                       |
                       |
                iface3:10.6.3.3   iface2:
             #################### 10.6.2.3        ##################
             self - rid: 10.6.0.3 --------------- r2 - rid: 10.2.0.3
             ####################        10.6.2.2 ##################
     iface1:10.6.1.3     iface0:10.6.0.3      10.2.0.3
            /                     \               /
           /                       \             /
     10.6.1.2                    10.6.0.2    10.2.0.2
##################                ##################
r1 - rid: 10.1.0.3                r0 - rid: 10.0.0.3
##################                ##################
       10.1.0.3                  10.0.0.3
           \                       /
            \                     /
           10.1.0.2          10.0.0.2
               ##################
               r3 - rid: 10.3.0.3
               ##################
```
You must also have a routing entry for `50.64.3.7` that does not have a corresponding arp cache entry.

# Control-Plane Baseline Tests

The control-plane baseline tests are located in [sanity_check.py](https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18/blob/master/contrib-projects/sume-sdnet-switch/projects/simple_router/sw/simple_router_sw/simulation/sanity_check.py#L108). This file also contains some baseline tests for the [PWOSPF functionality](https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18/blob/master/contrib-projects/sume-sdnet-switch/projects/simple_router/sw/simple_router_sw/simulation/sanity_check.py#L216).

It is possible that, although a new control plane is instantiated for each test, your state will not be fully cleared before the start of each test. If you encounter this issue, simply clear state in `setUp`.

# Submission

When you are ready to submit, tag the appropriate commit. Please include a description of who did what in the commit message.

```
$ git tag -a router-baseline -m "Submission of my simple_router basline functionality. <Description of who did what>"
$ git push origin router-baseline
```

The instructors will clone your repository and checkout the commit to which this tag points. We will then run your code and ensure that all of the baseline tests are passing.
