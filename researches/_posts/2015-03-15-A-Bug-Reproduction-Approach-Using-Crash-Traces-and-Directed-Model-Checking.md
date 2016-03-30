---
layout: post
title: A Bug Reproduction Approach Using Crash Traces and Directed Model Checking
tags:
- bug reproduction
- slicing
- model checking
- java
description: A Bug Reproduction Approach Using Crash Traces and Directed Model Checking
link: https://users.encs.concordia.ca/~abdelw/sba/papers/SANER2015-JCharming.pdf
excerpt: Maiga, A., Hamou-Lhadj, W., Nayrolles, M. , Sabor, K. & Larsson, A. (2015)
---

*Nayrolles, M. , Hamou-Lhadj, W., Tahar, S. & Larsson, A. (2015). A Bug Reproduction Approach Using Crash Traces and Directed Model Checking. International Conference on Software Analysis, Evolution, and Reengineering (SANER'15). (pp. 101-110). IEEE. Best Paper Award.*

—Due to their inherent complexity, software systems are pledged to be released with bugs. These bugs manifest themselves on client's computers, causing crashes and undesired behaviors. Field crashes, in particular, are challenging to understand and fix as the information provided by the impacted customers are often scarce and inaccurate. To address this issue, there is a need to find ways for automatically reproducing the crash in a lab environment in order to fully understand its root causes. Crash reproduction is also an important step towards developing adequate patches. In this paper, we propose a novel crash reproduction approach, called JCHARMING (Java CrasH Automatic Reproduction by directed Model checkING). JCHARMING uses crash traces and model checking to identify program statements needed to reproduce a crash. Our approach takes advantage of the completeness provided by model checking while ignoring unneeded system states by means of information found in crash traces combined with static slices. We show the effectiveness of JCHARMING by applying it to seven different open source programs cumulating more than one million lines of code scattered in around 7000 classes. Overall, JCHARMING was able to reproduce 85% of the submitted bugs

[pdf link](https://users.encs.concordia.ca/~abdelw/sba/papers/SANER2015-JCharming.pdf)
