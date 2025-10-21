---
title: "Real-Time Nuclei Classification and Allred Scoringin PR-IHC Stained Breast Cancer Histopathology Images"
collection: publications
category: conferences
permalink: /publication/real-time-breast-cancer
excerpt: ''
date: 2025-10-01
venue: 'Phuket, Thailand, In Proceedings of the International Conference on Information Technology (InCIT 2025). IEEE (Scopus Indexed)'
# slidesurl: 'http://academicpages.github.io/files/slides2.pdf'
# paperurl: 'http://academicpages.github.io/files/paper2.pdf'
citation: ' Bannah. H., Fauzi, M. F. A., Nabi, M. S., et al. (2025). Real-Time Nuclei Classification and Allred Scoringin PR-IHC Stained Breast Cancer Histopathology Images. In Proceedings of the International Conference on Information Technology (InCIT 2025). IEEE (Scopus Indexed).  Accepted]'
---
Progesterone receptor immunohistochemistry (PR-IHC) of breast cancer tissue requires precise nuclei classification and Allred scoring for biomarker quantification and clinical decision-making. However, these tasks are still difficult because of overlap, heterogeneous nuclear morphology, and  ariations in diaminobenzidine (DAB) staining. Using auto-calibrated DAB-intensity thresholds, we propose a real-time, lightweight framework for classifying individual nuclei into Strong, Moderate, Weak, and Negative categories. The pipeline separates the DAB signal, extracts nuclear contours,  ggregates per-nucleus intensity, and uses calibrated, intensity-driven decision-making to assign a single label. By combining the percentage of positive nuclei with their dominant staining intensity, we calculate ROI-level Allred scores, building on the nucleus-level outputs. The University of Malaya Medical Centre (UMMC) provided the primary dataset, and a hybrid automated–manual workflow with expert validation was used to create pixel-based ground truth for 250 PR-IHC images. This approach consistently performs well on a held-out test split (macro-F1 = 0.948; overall IoU = 0.906). The results demonstrate the usefulness of intensitydriven,  omputationally efficient techniques for Allred scoring and nucleus  lassification in digital pathology workflows. Instant Allred scoring without sophisticated computation is made possible by the lightweight design, which makes it appropriate for overloaded hospitals and clinics with limited resources. 