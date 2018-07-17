!SLIDE center subsection blue

# Git and GitLab

!SLIDE bullets

# Git

* Version Control Software
* Build by Linus for Linux
* Used everywhere, including the Windows kernel

!SLIDE bullets

# Controlling Change

* Put the DPK code into a Git repository
* Manage changes to DPK and YAML files
* Custom modules as Git sub-modules
* View history

!SLIDE bullets

# Git Branching

* Test changes on a branch
* Work on changes without impacting the main code line
* Assign branches to servers

!SLIDE bullets

# Git in Action

    @@@powershellconsole
    C:\> [856] git status
    On branch 856
    Changes not staged for commit:

            modified:   modules/mpls_profile/manifests/mpls_prcs.pp

    Untracked files:
      
            modules/mpls_deploy/manifests/mpls_nvision.pp

!SLIDE bullets

# Git in Action

    @@@powershellconsole
    C:\> [856 +1 ~1 -0 !] git add
    C:\> [856 +1 ~1 -0 ~] git commit -m "Create mpls_nvision class"
    [856 4ed3d2b] Create mpls_nvision class
    2 files changed, 24 insertions(+)
    create mode 100644 modules/mpls_deploy/manifests/mpls_nvision.pp

!SLIDE bullets

# Git in Action 

    @@@powershellconsole
    C:\> [856] git push origin 856
    Counting objects: 9, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (9/9), done.
    Writing objects: 100% (9/9), 1.06 KiB | 0 bytes/s, done.
    Total 9 (delta 5), reused 0 (delta 0)
    remote:
    remote: To create a merge request for 856, visit:
    remote:   https://gitlab.minneapolis.mn/dpk/merge_requests/new?merge_request%5Bsource_branch%5D=856

!SLIDE center subsection blue

# GitLab

!SLIDE bullets

# GitLab

GitLab is a DevOps Platform

* Code Management
* Continuous Integration/Deployment
* Issues Management
* Planning Tools
* Code Review
* Release Management
* System Monitoring
* Open Source (Monthly Releases)

!SLIDE bullets

# GitLab

We use GitLab for:

* Code Management
* Continuous Integration
* DPK Issue Tracking

!SLIDE bullets

# GitLab - Commit History

![GitLab Commit History](../_images/gitlab01.png)

!SLIDE bullets

# GitLab - Merge Requests

![GitLab Merge Requests](../_images/gitlab02.png)

!SLIDE bullets

# GitLab - Contributers

![GitLab Contributers](../_images/gitlab03.png)
