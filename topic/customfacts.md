!SLIDE center subsection blue

# Custom Facts

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

!SLIDE bullets

# Dynamic Server Builds

We have one `site.pp` for all servers:

    @@@ruby
    node default {
      case $facts[ps_role] {
        'app':   { include ::mpls_role::mpls_app }
        'prcs':  { include ::mpls_role::mpls_prcs }
      }
    }