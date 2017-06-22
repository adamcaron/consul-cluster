# Consul Cluster

An example Docker stack file that runs in a Docker Swarm cluster.

Depends on a Traefik reverse proxy to route requests to :8500.

Endpoint mode `dnsrr` adds an a-record with the exact same name (ex. consul) for each container's ip.  A reverse proxy is needed to route requests to the service (in this case, labels are used to tell Traefik to route requests with PathPrefix 'ui' or 'v1' to :8500).

`-disable-host-node-id` ensures the consul cluster can stand up on a single-node/single-host Docker Swarm.  Default behavior is that Consul generates a consul-node-id via the host's kernal and assumes each Consul node will be on a separate host.  To avoid duplicate IDs when running the Consul cluster on a single node, the `-disable-host-node-id` flag esures a random node id is generated instead of using information from the host's kernal.

Mounts each consul cluster container's data into folders named `/1`, `/2`, and `/3` correlating with each consul cluster task's slot number.  This depends on directories named `/1`, `/2`, and `/3` already existing at `./`

