# haproxy-consultemplate
simple (?) consul-template for HAProxy to allow it to work nicely with consul.

This scans for all services with the tag "proxy" then adds a LB rule for them.  Following additional behaviors worth noting:

* RUBY VARIABLES <%= @target_domain %> AND <%= @ipaddress %> must equal the served domain suffix and IP address of haproxy.
* <%= @wildcardcertpath %> should probably be replaced with your own wildcard certificate
* consul kv store is searched for "service/<servicename>" for overriding values incase defaults arn't correct.
* "balance_addport" is an addiional port number to LB (not on 443, but as passthrough)
* "balance_type" overrides the default roundrobin mode (usually to "source")
* "balance_addserveroptions" inserts said strign directly into the backend server options.  Catch-all for things like timeout
  
Note as this is using consul, there are no checks generated, as it assumed your checks are dfined and monitored in consul itself.
