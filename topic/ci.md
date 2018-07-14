!SLIDE center subsection blue

# Continuous Integration

!SLIDE bullets

# Continuous Integration

is the practice of merging all developer working copies to a shared mainline several times a day.

* includes automated testing of merged code

!SLIDE bullets

# GitLab and CI

* GitLab has integrated CI tools
* GitLab Runner execute tests
* Per-repository testing

!SLIDE bullets incremental

# How do we add CI to the DPK?

* DPK Testing Servers
* Define a test scenario to build
* Deploy GitLab Runners
* Push Git commits to GitLab
* Create Merge Request
* Verify test build
* Complete Merge Request

~~~SECTION:notes~~~
There are different workflows you can create for CI testing. Often times you want to verify the incoming code via CI before committing the change the repo. Or you can take merge requests into a testing branch and the execute your CI tests.
~~~ENDSECTION~~~

!SLIDE bullets

# DPK Continuous Integration

![DPK Pipeline Jobs](../_images/ci01.png)

!SLIDE bullets

# DPK Continuous Integration

![DPK CI Test](../_images/ci02.png)

!SLIDE bullets

# .gitlab-ci.yaml

* Defines your pipeline for a repo
* Create multiple CI jobs
* Assign actions for branches

!SLIDE bullets

# .gitlab-ci.yaml

    @@@yaml
    test:fs:
      stage: test
      only:
      - develop
      tags:
      - fs
      - admin
      script:
      - stop-service Psft* -WarningAction SilentlyContinue
      - set-location e:/psoft/dpk/puppet
      - git pull origin develop
      - git submodule init; git submodule update
      - puppet apply .\manifests\site.pp --environment=fs92dev2 --confdir=e:\psoft\dpk\puppet