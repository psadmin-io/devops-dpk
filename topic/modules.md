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
3. Enable Data Bindings in `puppet.conf`
  
        @@@ini
        data_binding_terminus=none

!SLIDE bullets

# DPK-specific modules