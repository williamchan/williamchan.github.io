---
layout: post
title:  The state of cancer detection
date:   2021-08-11 14:00:00 -0800
---

Is currently abysmal but with some promising steps toward a better future. Although cervical, breast, and colorectal cancers are screened for, by the time they are diagnosed, [metastasis has already occurred 50%, 37%, and 56% of the time](https://youtu.be/RiNi9mj9Gn8?t=120), respectively. This is an awful status quo for screened cancers.

Most cancer deaths, [79%](https://youtu.be/RiNi9mj9Gn8?t=164), are due to cancers without standard screening procedures, and those cancers tend to have an even higher chance of metastasis at diagnosis: [81% for pancreatic, 80% for ovarian, 70% for esophageal](https://youtu.be/RiNi9mj9Gn8?t=225). These cancers often have no symptoms in the earlier stages. I have heard lucky anecdotes of people coincidentally getting scans in some part of their body where an early stage tumor was growing. Dumb luck has been the state of the art for unscreened cancers.

[*Lifetime risk of developing cancer is ~40%*](https://www.cancer.org/cancer/cancer-basics/lifetime-probability-of-developing-or-dying-from-cancer.html).

### Multi-cancer liquid biopsy screening

I am excited by multi-cancer liquid biopsy screening. Galleri from Grail is a blood test that can detect 50 different types of cancer as early as stage 1. It can return a “suspicion of cancer” result along with tissue of origin (TOO). From their [2020 paper](https://www.annalsofoncology.org/article/S0923-7534%2820%2936058-0/fulltext), 50 types of cancer can be detected with **43.9% sensitivity in stage 1 to 3**. Sensitivity is what medical folks call recall, and it means that if cancer is present, it will be detected 43.9% of the time. The study quotes a 99% specificity (1% chance of false positive) and an impressive 93% accuracy on the tissue of origin if cancer is present.

*This is amazing data*. A sensitivity of 43.9% for detecting 50 cancers in stages 1 to 3 is way better than the status quo of zero screening. Galleri is not FDA approved and costs $949. I consider this worth ordering once a year for my loved ones of age 50+. Although I have questions I hope will be addressed in the future, they are the kinds of questions that can answered by Galleri getting more data.

The Galleri model appears to be well-fitted. The validation performance (green) is comparable to the training performance (red). Absent is the classic sign of overfitting in which validation performance is worse than training performance. That is pretty cool.

<img style="margin-left: auto; margin-right: auto; border: 1px solid lightgray" src="/assets/grail-2020-figure-4.png"/>

There is room for improvement from more data. The confidence intervals of the validation set is quite wide. For example, the validation set only contains 1 or 2 data points for stage 2/3 kidney cancer, so the confidence intervals are almost 0% to 100%. The accuracy on tissue of origin for stage 1 of all cancers looks like it is ~74% to 98% based on 30 data points. More data will answer: how sensitivity is Galleri really at stage 1 versus stage 2 for a specific type of cancer, and how accurate is Galleri really at pinpointing a specific tissue of origin. As someone about to order Galleri for family members, I am highly interested in these answers.

A 93% accuracy on TOO allows for 7% chance of “dude where’s my cancer” because the actual TOO could be far from the predicted TOO. In the validation set:
- a case of pancreas/gallbladder cancer was incorrectly predicted as breast.
- 2 cases of anus cancer was incorrectly predicted as head and heck.
- several cases of upper GI, sarcoma, liver/bile duct, head and heck, colorectal, and bladder/urothelial cancer were incorrectly predicted as lung.

Unfortunately, TOO mispredictions are often not in an adjacent organ. A followup scan of the lungs will not surface a colorectal cancer. Because the number of data points for most cancer types is small, more data would at least improve the estimate of accuracy and maybe the actual [TOO predictor](https://www.annalsofoncology.org/cms/10.1016/j.annonc.2020.02.011/attachment/085d1b94-e2fa-490f-9beb-5dae150e2dd4/mmc3.pdf) as well.

**Does Grail consider data availability to be a bottleneck?** If so, I hope Grail can accelerate their data collection by tapping into a community of consumers willing to pay out-of-pocket for the Galleri test.

Another detail I found interesting is that the validation set is *balanced*. The sensitivity, specificity, and accuracy numbers were computed on a validation set of 1,264 of whom 654 had cancer and 610 did not. In machine learning class, we learn to use validation sets that reflect the real world, and the real world is not an almost 50/50 balance between cancer and not cancer. We also learn to use test sets in a workflow that looks like: train multiple models on a training set that might be balanced, then pick the best of the models based on performance on a validation set, and then use the test set to calculate the performance metrics you share with an admiring audience. In practice, teams work with what they have. With respect to Galleri, I wonder when performance metrics on a real world test set will be calculated, whether in STRIVE (ending 2025) or in SUMMIT (ending 2030) or in the general public after FDA approval.

At a high level, Galleri uses a laboratory technique called targeted methylation to turn blood samples into data. Given usable data, a software team can create a model to detect cancer. With time and effort, the software team will eventually produce an optimal model with the data available. At that point, creating a better cancer detection model is dependent on improving the data. Galleri uses targeted methylation to highlight locations where cytosine is followed by guanine, CpG sites, and a lot of DNA is not C-followed-by-G. It seems to me that DNA sequencing would produce data of higher fidelity than targeted methylation. As the cost of sequencing falls, I am interested in whether replacing targeted methylation with DNA sequencing will lead to cancer detection with much higher sensitivity and tissue of origin accuracy.

### Who I will be watching

Galleri is the third liquid biopsy on the market. [FoundationOne Liquid CDx](https://www.foundationmedicine.com/test/foundationone-liquid-cdx) and [Guardant360 CDx](https://guardant360cdx.com/) are liquid biopsies with FDA approval, both as companion diagnostics. A companion diagnostic is for identifying patients who can receive specific targeted drugs.

[Exact Sciences](https://thrivedetect.com) and [Freenome](https://www.freenome.com/) are developing liquid biopsies for cancer screening. There is nothing to try or buy yet, as of August 2021. A [2020 paper](https://science.sciencemag.org/content/369/6499/eabb9601) from Exact Sciences describes using two blood tests, a baseline test and a confirmation test, followed by a scan such as PET-CT. Their performance numbers are impressive, but data collection seems to progress slowly, with only 96 cancer data points collected out of 9,911 participants. [Earli](https://www.earli.com) is taking a different approach of manipulating cancer cells to produce synthetic biomarkers instead of looking for natural biomarkers.

Exact Sciences has a FDA approved test for colorectal screening called [Cologuard](https://www.cologuard.com/) that sounds amazing because it involves pooping instead of an exam up your butt. [Guardant](https://guardanthealth.com/clinical-studies/) is developing a blood test for colorectal cancer, and also evaluating whether their liquid biopsy for companion diagnostics can be useful for screening breast cancer.

### My screening and lifestyle plan

Having reviewed the standard screenings, liquid biopsies screenings, and risk factors for many cancers, I wrote this plan for screenings and minimizing risk factors. Limiting meat and alcohol are on here because they are common risk factors for several cancers (as is smoking).

| Lifestyle change | When |
| --- | ----------- |
| Give up meat | Everyday |
| Give up alcohol or set strict limits | Everyday |
| [Learn breast self-exam](https://www.breastcancer.org/symptoms/testing/types/self_exam) | Monthly at home |
| [Learn skin self-exam](https://www.cancer.org/healthy/be-safe-in-sun/skin-exams.html) | Monthly at home |
| [Learn testicular self-exam](https://www.cancer.org/cancer/testicular-cancer/detection-diagnosis-staging/detection.html) | Monthly at home |
| For 50+ relatives, order multi-cancer liquid biopsy screening from [galleri.com](https://www.galleri.com/) | Annually for relatives age 50+, $949 out-of-pocket |
| Get urine test at regular physical exam | Annually at doctor's office |
| Get blood test at regular physical exam | Annually at doctor's office |
| Regular colorectal exams at 45+. Ask for [Cologuard](https://www.cologuard.com/). | Annually at doctor's office at age 45+ |
| Women: Regular HPV and Pap tests | Annually at doctor's office |
| Women: Regular pelvic exams | Annually at doctor's office |
| Women: Regular breast exam | Annually at doctor's office at age 40+ |
| Men: Regular prostate exam at 55+ | Annually at doctor's office at age 55+ |

Here are my notes on several cancer types including 5-yr survival rates, median age of diagnosis, early signs, and controllable risk factors.

[<img style="margin-left: auto; margin-right: auto;" src="/assets/cancer-notes.png"/>](https://docs.google.com/spreadsheets/d/1619A3UWJcHtp9QFqogLaTCTIDBOmQNQCLTExMS3QYag/edit?usp=sharing)

[click to expand](https://docs.google.com/spreadsheets/d/1619A3UWJcHtp9QFqogLaTCTIDBOmQNQCLTExMS3QYag/edit?usp=sharing)
