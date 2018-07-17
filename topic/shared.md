!SLIDE center subsection blue

# Shared Directories

!SLIDE bullets incremental

# DPK Archive Methodology

* Each server is self-contained
* The archive on the server gets deployed
* Cannot store more than 1 version
* No knowledge of versions
* `get_matched_file()`

~~~SECTION:notes~~~
The `get_matched_file()` function is a custom DPK function that finds the middleware/software archives on your server. If there is more than 1 matching archive, it complains and returns an error.

Also, this function doesn't handle the OS path changes well. If you run Windows, but have a Puppet Server (linux), the `get_matched_file()` function doesn't know to use a linux path. It uses the path in the context of the catalog for the target machine.
~~~ENDSECTION~~~

!SLIDE bullets incremental

# Improving Archive Storage

* Centralize archive storage
* Store multiple versions of an archive
* Streamline the deployment process
* Reduce duplicate file storage

!SLIDE bullets

# Specifying Versions

* `psft_customizations.yaml`

        @@@yaml
        wl_version:             '12.2.1.3.0.20180417'
        tux_version:            '12.2.2.0.0'
        jdk_version:            '1.8.0_171'
        tools_version:          '8.56.08'

!SLIDE bullets

# archive_files Hash

* `psft_customizations.yaml`

        @@@ruby
        archive_location:       '\\\\server\share/dpk/archives'
        archive_files:
          weblogic:             "%{hiera('archive_location')}/pt-weblogic%{hiera('wl_version')}.tgz"
          tuxedo:               "%{hiera('archive_location')}/pt-tuxedo%{hiera('tux_version')}.tgz"
          jdk:                  "%{hiera('archive_location')}/pt-jdk%{hiera('jdk_version')}.tgz"


!SLIDE bullets

# Puppet Changes

* `puppet/modules/pt_setup/manifests/tools_deployment.pp`

        @@@ruby
        $archive_files = hiera('archive_files', '')

        if $archive_files {
          $weblogic_archive_file   = $archive_files[$weblogic_tag]
        } 
        if $weblogic_archive_file == '' {
          $weblogic_archive_file = get_matched_file($tools_archive_location, $weblogic_tag)
        }
        if $weblogic_archive_file == '' {
          fail("Unable to locate archive (tgz) file for Weblogic in ${tools_archive_location}")
        }