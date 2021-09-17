---
layout: post
title:  Detecting cancer with MRI
date:   2021-09-16 12:00:00 -0800
---

Since writing about [cancer detection with liquid biopsy](https://williamchan.github.io/cancer-detection.html), I have learned about comprehensive MRI scanning for cancer detection. [Prenuvo](https://www.prenuvo.com) offers full body MRIs for $3k in Redwood City, Minneapolis, and Vancouver. [Shuang Ho Hospital in Taipei](https://www.medicaltravel.org.tw/Hospital-Content.aspx?l=2&id=52) offers comprehensive health screening including scans. [Mayo Clinic](https://www.mayoclinic.org/departments-centers/mayo-clinic-executive-health-program/sections/executive-health-standard-protocol/gnc-20253373) has an executive health program, which I think includes some amount of scanning.

I consider [Galleri from Grail](https://www.galleri.com/) and full body MRI to be *complementary* approaches. You can elect to use all available tools for cancer detection and give your loved ones the kind of care that executives receive. Maybe scanning and liquid biopsy are good at detecting different signals. In terms of cost, a Galleri test at $1k is priced like a roadtrip, and a Prenuvo appointment at $3k is like a vacation with airfare.

MRI is **not** perfectly accurate for detecting cancer. For breast cancer, MRI has a specificity of 65.8%, or an awful 34.2% chance of false positive. For uterine and cervical cancer, specificity is 66.7% on a small sample size in which even a small change in the data would really swing the sensitivity and specificity numbers. For ovarian cancer, specificity is an even lower 33%. Here, where the signal-to-noise is far from perfect, you do not want to die from unnecessary biopsies.

This table has the sensitivity and specificity of MRI for detecting cancers, based on the [citations](https://www.prenuvo.com/physician/cancer-screening) on Prenuvo's website. I marked the low specificities and small sample sizes in <span style="color:red">red</span>.

| Cancer | Sensitivity | Specificity | n | Citation |
| ------ | ----------- | ----------- | - | -------- |
| breast | 98.7%	 | <span style="color:red">65.8%</span> | 143 | [29644993](https://pubmed.ncbi.nlm.nih.gov/29644993) |
| prostate | 69% | 89% | 5,892 | [22997374](https://pubmed.ncbi.nlm.nih.gov/22997374) |
| colorectal | 95% | 93% | 545 | [26770325](https://pubmed.ncbi.nlm.nih.gov/26770325) |
| ovarian | 98% | <span style="color:red">33%</span> | 51 | [27585490](https://pubmed.ncbi.nlm.nih.gov/27585490) |
| uterine cervical | 94.7% | <span style="color:red">66.7%</span> | <span style="color:red">38</span> | [26162579](https://pubmed.ncbi.nlm.nih.gov/26162579) |
| pancreatic | 93% | 89% | 5,399 | [28624015](https://pubmed.ncbi.nlm.nih.gov/28624015) |
| liver | 97% | 98% | <span style="color:red">44</span> | [22226435](https://pubmed.ncbi.nlm.nih.gov/22226435) |
| kidney | 91% | 89% | 158 | [29230706](https://pubmed.ncbi.nlm.nih.gov/29230706) |
| stomach, stage 1 | 75% | 84.6% | <span style="color:red">very small</span> | [28265229](https://pubmed.ncbi.nlm.nih.gov/28265229) |
| bladder | 94.5% | 87.5% | 102 | [29732204](https://pubmed.ncbi.nlm.nih.gov/29732204) |
| esophageal | 67% | 92% | <span style="color:red">42</span> | [27767330](https://pubmed.ncbi.nlm.nih.gov/27767330) |
| larynx | 81.8% | <span style="color:red">64.7%</span> | 50 | [23874693](https://pubmed.ncbi.nlm.nih.gov/23874693) |
| lymphoma | 100% | 91.7% | <span style="color:red">26</span> | [25952024](https://pubmed.ncbi.nlm.nih.gov/25952024) |
| lung   | 86.4% for size 6-9mm, 97% for ≥10mm, 43.8% for ≤5mm | 92.3%, 96%, and 80% | 71 | [21696559](https://pubmed.ncbi.nlm.nih.gov/21696559) |

My takeaways from reading this data...

**Cancers of the digestive tract**: Although sensitivity and specificity of MRI look good for pancreatic, liver, kidney, and stomach cancer, these numbers are not by stage. For pancreatic cancer, [imaging seems to often miss early tumors](https://www.nature.com/articles/d41586-020-00846-3). I have not been able to find MRI sensitivity numbers for stage 1/2/3 for these cancers. The [2021 paper from Grail](https://www.annalsofoncology.org/article/S0923-7534%2821%2902046-9/fulltext) does clearly show these numbers for their Galleri test: ~60% for pancreatic stage 1/2, ~50% for stomach stage 2 (on small sample size), and very high for liver and bile duct stage 1/2 (also small sample size). While I would like to see more data about detecting cancer early with Galleri and MRI, I have seen enough to believe that they are valuable and could be used in a complementary way.

**Cancers with lower signal-to-noise**: If the next test after "finding something" with MRI is an invasive and potentially dangerous biopsy, the right decision might not necessarily be to do that biopsy. Anecdotally, a friend was in this situation when a brain scan revealed something suspicious, not a cancer but a "something." The next test is literally a brain surgery. In the case of this friend, a subsequent brain scan after a few years showed no change, and no unnecessary brain surgeries were done. I would keep this in mind for cancer types with lower specificity numbers, like breast and ovarian.

I am new at reading and thinking about this topic. I have no medical background. I am just trying to do right for my family. While reading, I noticed two conventional wisdoms about scanning. One is that a lot of the discussion about the feasibility of scanning is at the policy level. The American healthcare system cannot afford to give full body MRIs to everyone over 50. Besides the financial considerations, there is concern about the excess mortality from unnecessary biopsies if hospitals started to scan every patient. I am not writing a policy article here. I am considering full body MRI from a personal perspective.

The second piece of conventional wisdom has to do with the limitations of MRI data due to its noisiness. From a computer science perspective, even noisy data is useful. There should be great value in seeing how scans change for an individual at age 40 versus 45, 50, 55, 60, and so on. Get that first set of scans while that person is younger and healthier to establish a baseline. At the industry level, if substantially more MRI data were generated, there would be greater incentive to innovate the scanning hardware and the detection software, improving the quality and usefulness of MRI data and driving down the cost per scan. Not that I am holding my breath for this to play out in the medical imaging industry, but I think many computer scientists would agree that even noisy data can be valuable.

*For reference, figure 3 from [Grail's 2021 paper](https://www.annalsofoncology.org/article/S0923-7534%2821%2902046-9/fulltext)*:
<img style="margin-left: auto; margin-right: auto;" src="/assets/grail-2021-figure-3.png"/>
