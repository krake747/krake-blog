---
hide:
  - toc
tags:
  - Git
---

# Git Strategies

**Trunk-Based Development** (TBD) is a simpler approach where everyone works on a single `main` branch. 
Changes are merged frequently, ensuring continuous integration and faster feedback. 
Additionally, TBD often incorporates feature management techniques, such as feature flags, to enable controlled deployment and experimentation of new features.

**Git Flow** uses multiple branches (`master`, `develop`, `feature`, etc.) for different stages of development, 
offering a more structured workflow but potentially slower feedback loops. This is a legacy Git workflow, Trunk-Based Development should be the preferred choice. 