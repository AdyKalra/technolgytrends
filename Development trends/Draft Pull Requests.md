**When you create a Draft Pull Request, it cannot be merged until it is marked as ready for review. This is useful because often pull requests are used as conversations, often prior to the work being ready to merge.** 

Common approaches to this in the past have included such classic approaches as:
* Adding “WIP” for “Work in Progress” to the PR title
* Adding “DO NOT MERGE” to the title (or description, tag, etc.)


In some cases, whole bot-based workflows were set up to look for things like “WIP” in PR names and to take actions like marking the PR as not approved until the label was removed or updated.

Draft pull requests essentially do away with the need for such hacks. Now when you create a pull request, you have the option (via the dropdown button) to create a draft pull request instead:

![PR](https://ardalis.com/static/b67d6c611f2ee03eb32fde0119712444/23296/pull-request.png)

