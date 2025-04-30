---
author: ckanyika
ms.author: ckanyika
ms.date: 4/3/2025
ms.topic: include
---

### GitHub Integration: Improvements linking to commits, branches and pull requests

We're continuously improving the Boards + GitHub integration to close usability gaps and align with the experience you're familiar with in Azure Repos.

With this update, we've introduced several improvements to streamline how branches, pull requests, and commits are linked to work items:

* When a GitHub branch is linked to a work item, any associated pull requests will now be automatically linked. No need to manually use AB#.

* Once a pull request is merged, the merge commit will be automatically linked to the work item.

* If the branch is deleted after the pull request is merged, the branch link will be automatically removed from the work item.

These improvements make it easier to track your development progress and maintain clean, up-to-date work item associations.


> [!div class="mx-imgBorder"]
> ![Gif to github boards integration improvements.](../../media/254-boards-01b.gif "gif to github boards integration improvements")

### GitHub Integration: Show build status for YAML pipelines

We're committed to achieving feature parity between YAML and Classic Pipelines. One key missing feature was the ability to provide an "Integrated in build" link when your repository is hosted in GitHub. With our latest release, we've addressed this gap by adding an option in YAML pipeline settings for you to check:

> [!div class="mx-imgBorder"]
> [![Screenshot of automatically link work items.](../../media/254-boards-01.png "Screenshot of automatically link work items")](../../media/254-boards-01.png#lightbox)

Once the build is complete, the corresponding link will automatically appear on the associated work items, improving the overall traceability story.

> [!div class="mx-imgBorder"]
> [![Screenshot of integrated in build.](../../media/254-boards-02.png "Screenshot of integrated in build")](../../media/254-boards-02.png#lightbox)

### Delivery Plans limit increased

Previously, we limited the Delivery Plans per project to 1,000. With this update, we have increased the maximum Delivery Plans per project to 1,500. You can learn more about adding and editing Delivery Plans in the documentation [here](https://learn.microsoft.com/azure/devops/boards/plans/add-edit-delivery-plan?view=azure-devops).
