!SLIDE center subsection blue

# Puppet Environments

!SLIDE bullets

# DPK Limitations

The DPK was designed to run 1 PeopleSoft environment on a server.

* Too much server sprawl for us
* Breaks our current infrastructure design
* DPK is not idempotent

~~~SECTION:notes~~~
The DPK was primarily built for PeopleSoft Images and Oracle Cloud. Single server, contained installations. Like lots of orgs, we co-locate many of our PS environments on the same server.
~~~ENDSECTION~~~

!SLIDE bullets

# Puppet Environments

Puppet Environments let you segregate:

* Configuration
* Modules
* Target Software

!SLIDE bullets

# Puppet Environments

This enables us to separate

* HRDEV
* HRTST
* HRDMO

while running on the same server

!SLIDE bullets incremental

# Puppet Environments

Supported in 8.55 and 8.56 (easier in 8.56)

1. Add `environmentpath` and `basemodulepath` to `puppet.conf`

        @@@yaml
        environmentpath=e:\psoft\dpk\puppet\environments
        basemodulepath=e:\psoft\dpk\puppet\modules

1. Update `hiera.yaml` to use the `%{::environment}` fact for`psft_customizations.yaml`

        @@@yaml
        :hierarchy:
          - "environments/%{::environment}/data/psft_customizations"

1. Call `puppet apply` with `--environment hrdev`

!SLIDE center subsection blue

# Demo

~~~SECTION:notes~~~
Use ELMTST to demonstrate how the DPK can be used on one environment without disturbing others.
~~~ENDSECTION~~~

!SLIDE bullets

# Puppet Environments

Puppet Environments let us:

* Perform maintenance on one environment without shutting down everything
* Test modules on a specific environment first
* Keep our co-located environments
* Reduce server sprawl and better utilize hardware

