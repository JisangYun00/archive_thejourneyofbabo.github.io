---
title: Lab4_Follow_the_Gap
draft: false
tags:
  - F1Tenth
aliases:
---
## Following the Gap
> [Lecture_Note](https://docs.google.com/presentation/d/1icJ0SHz2Q6JybGRywRTIHEpZbuQ_K2lmvEoJ-sYO4C4/edit#slide=id.p22) / [Our Code](https://github.com/thejourneyofbabo/f1sim_ws/tree/master/src/lecture_ws/f1tenth_lab4_template)
### Method
![[Follow the gap Tweak1.png]]
### Adaptive Scan-Threshold
> **Adjusting Scan Treshold with minimum range**
``` cpp
            {0.15, 0.4},  // Min
            {0.2, 0.8},   
            {0.5, 1.4},   
            {0.8, 1.8},
            {1.1, 2.4},
            {1.4, 2.8},   // Middle range
            {1.7, 3.2},
            {2.0, 3.6},
            {2.3, 3.9},
            {2.6, 4.2},
            {3.0, 4.5}    // Max

```

> **Limit the View angle**
```cpp
    double left_wing = M_PI / 2.7;
    double right_wing = -(M_PI / 2.7);

```
### Simulation Workspace
This is with Bubble Method
![[Follow-the-Gap-levine-obs.gif]]
![[Gap_follow_sim(obs).gif]]

**Race Track Map**
![[Gap_Follow_sim(2025.02.09).gif]]
### Real World Test
![[gap-follow-test.mp4]]

**- Next -**


---
### Reference
[F1Tenth_Lab4_Template](https://github.com/f1tenth/f1tenth_lab4_template)
[Disparity Node Method](https://www.nathanotterness.com/2019/04/the-disparity-extender-algorithm-and.html)
[disparity Node Github](https://github.com/pmusau17/Platooning-F1Tenth?tab=readme-ov-file)