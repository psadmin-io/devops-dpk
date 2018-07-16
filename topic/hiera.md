!SLIDE center subsection blue

# Hiera Hashing

!SLIDE bullets

# Duplicate Data

The delivered Hiera configuration encourages duplicate data. You redefine:

1. Domain defaults
1. Locations and folders
1. 

!SLIDE bullets

# Hierarchy
 
    @@@yaml
    :hierarchy:
      - "data/servers/%{::hostname}"
      - "data/database/%{::environment}"
      - "data/appregion/%{::app}%{::region}" 
      - "data/region/%{::region}"
      - "data/app/%{::app}"
      - data/acm
      - data/domains
      - data/common
