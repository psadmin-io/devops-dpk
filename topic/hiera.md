!SLIDE center subsection blue

# Hiera Hashing

!SLIDE bullets

# Duplicate Data

The delivered Hiera configuration encourages duplicate data. You redefine:

1. Domain defaults
1. Locations and folders
1. User names
1. Application specific config

!SLIDE bullets

# Hiera Hash Merging

1. Native Merge - Top Level Keys Only
1. Deep Merge   - Recursive Merge 

DPK uses the **Native Merge** method.

~~~SECTION:notes~~~
This is why you have to copy the entire `*_domain_list` hash with the DPK.
~~~ENDSECTION~~~

!SLIDE bullets

# Convert to Deep Merge (Hiera Hashing)

1. Find: `hiera('tns_admin_list`
1. Replace: `hiera_hash('tns_admin_list`

Repeat for these hashes:

* `tns_admin_list`
* `appserver_domain_list`
* `prcs_domain_list`
* `pia_domain_list`
* `component_preboot_setup_list`
* `component_postboot_setup_list`

~~~SECTION:notes~~~
There is a blog post on this topic as well.
~~~ENDSECTION~~~

!SLIDE bullets

# Convert to Deep Merge (Hiera Hashing)

* `dpk\puppet\hiera.yaml`

Add this line to the file:

    @@@yaml
    :merge_behavior: deeper

!SLIDE bullets

# Rethink the Hiera Hierarchy

Once you can merge hashes, you don't need one big `psft_customizations.yaml` file. You can separate:

* Common config
* Domain default config
* Per-application config
* Per-server config
* Per-database config
* and more!

!SLIDE bullets

# Hierarchy
 
    @@@yaml
    :hierarchy:
      - "servers/%{::hostname}"
      - "database/%{::environment}"
      - "appregion/%{::app}%{::region}"
      - "region/%{::region}"
      - "app/%{::app}"
      - "acm"
      - "domains"
      - "common"

!SLIDE bullets

# Hiera Hashing Advantages

Using the Deep Merge for Hiera gives us:

* Standard domain configuration
* Far less effort to create new domains
* Easier changes to common configuration
* Leverage server names to drive configuration