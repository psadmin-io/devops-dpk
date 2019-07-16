!SLIDE bullets

# Devops

The main characteristic of the DevOps movement is to strongly advocate automation and monitoring at all steps of software construction, from integration, testing, releasing to deployment and infrastructure management.

!SLIDE bullets incremental

# Devops and the DPK

How do these fit together?

Focus on:

* Managing PeopleSoft servers via code
* Follow a development lifecycle for code changes
* Test our Infrastructure as Code
* Provide flexibility in PeopleSoft deployments

~~~SECTION:notes~~~
With these goals in mind, we end up with some changes to the delivered DPK that get us the flexibility and "Infrastructure as Code" style deployments with PeopleSoft.
~~~ENDSECTION~~~


!SLIDE bullets

# Agenda

1. Git and GitLab
1. Continuous Integration
1. Shared Directories
1. Custom Facts
1. Hiera Hashing
1. Puppet Environments
1. Custom DPK Modules

!SLIDE bullets

# DPK Experience

To get the most from this talk:

* Experience with the DPK beyond PeopleSoft Images
* Used the `psft_customizations.yaml` file
* Used the DPK on your own environments

This is a talk based on DPK experience and contains advanced topics.

~~~SECTION:notes~~~
This talk is intended for an experienced admin with DPK background. These are changes we make to the DPK based on our experience to make it a better tool.
~~~ENDSECTION~~~
