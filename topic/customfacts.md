!SLIDE center subsection blue

# Custom Facts

!SLIDE bullets

# Controlling Actions

The DPK allows you to:

* Run the ACM
* Redeploy middleware

a.k.a - tasks you don't want to do every time

!SLIDE bullets

# Controlling Actions

To specify a single redeploy

1. Change `psft_customizations.yaml`'s `redeploy` variable
1. Commit the change
1. Push the change to the servers
1. Run the redeploy
1. Undo the `redeploy` variable
1. Commit the change
1. Push the change to the servers

*Data files should not be transactional*

!SLIDE bullets incremental

# Using Custom Facts

* Custom fact to return `false` for the `::redeploy` fact
* Set `redeploy: "%{::redeploy}"` in `psft_customizations.yaml`
* Override custom facts with environment variable

        @@@powershellconsole
        PS> $env:FACTER_redeploy="true"
        PS> puppet apply .\site.pp 

!SLIDE bullets

# Using Custom Facts

* `dpk/modules/mpls_role/lib/facter/redeploy.rb`

        @@@ruby
        Facter.add(:redeploy) do
          setcode do
            'false'
          end
        end

!SLIDE bullets

# Controlling Actions

To specify a single redeploy

1. Set `$env:FACTER_redeploy` in Powershell
1. Run `puppet apply`
1. Close Powershell

~~~SECTION:notes~~~
Or, substitute Powershell with a script, and run that script from Rundeck for part of your CPU patching process.
~~~ENDSECTION~~~

!SLIDE bullets

# Dynamic Server Builds

Servers are named based on:

* Function
* Location
* Application

For example:

* Web/App or Prcs
* Dev, QA, Prod
* HR/ELM or FS

!SLIDE bullets

# Custom Server Name Facts

* `ps_role`
* `region`
* `app`

!SLIDE bullets

# Custom Server Name Facts

    @@@ruby
    Facter.add(:ps_role) do
      setcode do
        hostname = Facter.value(:hostname)  
        ps_role = hostname.downcase.match(/app|prcs/).to_s
        if hostname.downcase.match(/admin/)
          ps_role = "app"
        end
        ps_role
      end
    end

~~~SECTION:notes~~~
We'll see more of the custom facts next when we look at Hiera.
~~~ENDSECTION~~~
