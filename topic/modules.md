!SLIDE center subsection blue

# Custom DPK Modules

!SLIDE bullets

# Custom DPK Modules

* Fill in DPK gaps
* Started by Eric Bolinger (CU/Oracle)
* Make it your system, not a Demo environment
* Open Source (github.com/psadmin-io)
* Windows and Linux support

!SLIDE bullets

# io_weblogic

WebLogic Domain Configuration

* Certificates 
* Java Options 
* pskey
* JCE
 
!SLIDE bullets

# io_portwar

Website Configuration

* configuration.properties
* Cookie Name 
* Index Redirect
* text.properties
* Custom Signon
  
!SLIDE bullets

# Install Modules

1. `git clone https://github.com/psadmin-io/psadminio-io_portalwar`
1. `git submodule add https://github.com/psadmin-io/psadminio-io_portalwar; git submodule init`
2. `puppet module install psadminio_io_portal` (future)

!SLIDE bullets

# Configuring DPK Modules

    @@@yaml
    io_weblogic::java_options:
      "%{hiera('db_name')}":
        -Xms:                              '512m'
        -Xmx:                              '512m'
        -Dweblogic.threadpool.MinPoolSize: '=50'
        -Dweblogic.security.SSL.protocolVersion:  '=TLSv1.2'
        -Dtuxedo.jolt.LLEDeprecationWarnLevel:    'NONE'

!SLIDE bullets

# Configuring DPK Modules

    @@@yaml
    io_portalwar::source: 'puppet:///modules/mpls_deploy'
    io_portalwar::signon_page:
      "%{hiera('db_name')}":
        root:
          - f5.html
          - robots.txt
        portal:
          - bootstrap.min.css
          - bootstrap.min.js
          - jquery-1.11.3.min.js
        psftdocs:
          - comet.html

!SLIDE bullets

# Calling DPK Modules

    @@@ruby
    class mpls_profile::mpls_pia {
      notify { 'Applying mpls_profile::mpls_pia': }

      require pt_profile::pt_pia

      contain ::io_weblogic
      contain ::io_portalwar
    }