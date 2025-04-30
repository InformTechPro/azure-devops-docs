---
author: ckanyika
ms.author: ckanyika
ms.date: 3/20/2025
ms.topic: include
---

### Publish code coverage results v2 task improvements

With this release we're including several improvements to the v2 task:
* Expanded support for various code coverage formats, including: .coverage,.covx,.covb,.cjson,.xml,.lcov, and pycov1.
* Generation of a comprehensive cjson file (and a Code Coverage report) that contains detailed code coverage information such as file names, lines covered/not covered, etc.

> [!div class="mx-imgBorder"]
> [![Screenshot of code coverage.](../../media/253-testplans-01.png "Screenshot of code coverage")](../../media/253-testplans-01.png#lightbox)

* Support for diff coverage (PR coverage): v2 can generate diff coverage PR comments for multiple languages within the same pipeline.
* v2 task now supports the Build Quality Check task, which wasn't supported in v1 task.

### Export test cases with custom columns in XLSX

You can now export test cases with custom columns in XLSX. Based on your feedback, Test Plans supports exporting test cases with custom columns, giving you greater flexibility and control over the data you share and analyze. This enhancement helps you tailor exports to your needs, ensuring the information you export is relevant and actionable.
