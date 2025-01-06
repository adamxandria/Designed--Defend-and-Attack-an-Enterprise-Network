Overview  
Our team has implemented a number of security configurations in our various network devices to prevent our network against threats and attacks.  
  
List of defenses configured  
-Port security --> Limit traffic on individual switchports  
-DHCP snooping --> Prevents DHCP related attacks  
-ARP inspection --> Prevent ARP related attacks  
-IPSG --> Prevents IP/MAC spoofing attacks  
-BPDU guard --> Prevent BPDU related attacks   
-Disable unused services  
-Shutdown unused ports and place in a seperate VLAN  
-Logging --> Monitors activity on devices  
-AAA --> FreeRadius used, access control and logging  
-ACL --> Access control to filter traffic  
-Deny ICMP (Pinging) 
-Login block when possible DOS detected 

ACL configurations:  
access-list OUTBOUND_INBOUND remark Jumphost ACL
access-list OUTBOUND_INBOUND extended permit tcp any object obj-jumphost eq ssh
access-list OUTBOUND_INBOUND remark Webserver ACL
access-list OUTBOUND_INBOUND extended permit tcp any object obj-web-server eq www
access-list OUTBOUND_INBOUND extended permit tcp any object obj-web-server eq https
access-list INBOUND_TO_OUTBOUND remark Visitor Kiosks ACL
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-visitor-kiosks object obj-web-server eq www
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-visitor-kiosks object obj-web-server eq https
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-visitor-kiosks object obj-dns-server eq 53
access-list INBOUND_TO_OUTBOUND extended deny ip object obj-visitor-kiosks any
access-list INBOUND_TO_OUTBOUND remark Facilities & Event Management (RESTRICTED STAFF)
access-list INBOUND_TO_OUTBOUND extended deny ip object obj-facilities-event-mgmt-restricted object-group objgrp-restricted-user-network
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-facilities-event-mgmt-restricted object obj-web-server eq www
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-facilities-event-mgmt-restricted object obj-web-server eq https
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-facilities-event-mgmt-restricted any eq www time-range non-work-hours
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-facilities-event-mgmt-restricted any eq https time-range non-work-hours
access-list INBOUND_TO_OUTBOUND extended deny ip object obj-facilities-event-mgmt-restricted any
access-list INBOUND_TO_OUTBOUND remark Facilities & Event Management (UNRESTRICTED STAFF)
access-list INBOUND_TO_OUTBOUND extended deny ip object obj-facilities-event-mgmt-unrestricted object-group objgrp-unrestricted-user-network
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-facilities-event-mgmt-unrestricted any eq www
access-list INBOUND_TO_OUTBOUND extended permit tcp object obj-facilities-event-mgmt-unrestricted any eq https
access-list INBOUND_TO_OUTBOUND extended deny ip object obj-facilities-event-mgmt-unrestricted any
access-list INBOUND_TO_OUTBOUND remark IT Department
access-list INBOUND_TO_OUTBOUND extended permit ip object obj-it-dept any






