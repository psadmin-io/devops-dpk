!SLIDE center subsection blue

# 

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
