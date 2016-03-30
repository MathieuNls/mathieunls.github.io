---
layout: post
title: Improving SOA Antipatterns Detection in Service Based Systems by Mining Execution Traces
tags:
- java
- antipatterns
- automatic detection
- SOA
description: Improving SOA Antipatterns Detection in Service Based Systems by Mining Execution Traces
link: https://www.computer.org/csdl/proceedings/wcre/2013/9999/00/06671307.pdf
excerpt: Nayrolles, M. , Moha, N. & Valtchev, P. (2014).
---

*Nayrolles, M. , Moha, N. & Valtchev, P. (2014). Improving SOA Antipatterns Detection in Service Based Systems by Mining Execution Traces. Working Conference on Reverse Engineering. (pp. 321-330). IEEE.*

Service Based Systems (SBSs), like other software systems, evolve due to changes in both user requirements and execution contexts. Continuous evolution could easily deteriorate the design and reduce the Quality of Service (QoS) of SBSs and may result in poor design solutions, commonly known as SOA antipatterns. SOA antipatterns lead to a reduced maintainability and reusability of SBSs. It is therefore important to first detect and then remove them. However, techniques for SOA antipattern detection are still in their infancy, and there are hardly any tools for their automatic detection. In this paper, we propose a new and innovative approach for SOA antipattern detection called SOMAD (Service Oriented Mining for Antipattern Detection) which is an evolution of the previously published SODA (Service Oriented Detection For Antpatterns) tool. SOMAD improves SOA antipattern detection by mining execution traces: It detects strong associations between sequences of service/method calls and further filters them using a suite of dedicated metrics. We first present the underlying association mining model and introduce the SBS-oriented rule metrics. We then describe a validating application of SOMAD to two independently developed SBSs. A comparison of our new tool with SODA reveals superiority of the former: Its precision is better by a margin ranging from 2.6% to 16.67% while the recall remains optimal at 100% and the speed is significantly reduces (2.5+ times on the same test subjects).

[pdf link](https://www.computer.org/csdl/proceedings/wcre/2013/9999/00/06671307.pdf)
