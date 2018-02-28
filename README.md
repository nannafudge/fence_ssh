# fence_ssh
Fencing agent that uses SSH, should only be used for testing.

Can easily be modified so you only need one fence_ssh resource per cluster (remove hostname arg, change to nodename), although this means you can't use the monitor function and will have to comment it out.

# How to Use
Place in /usr/sbin with execute permissions

Create stonith resources in Pacemaker

Can see usage with either fence_ssh --help or by running pcs stonith describe fence_ssh

Example usage with PCS:

_Ensure that pcmk_host_list is defined so that Pacemaker knows which resource can fence which node_
pcs stonith create stonith-one fence_ssh user=centos hostname=host1 password=Pa55w0rd sudo=true pcmk_host_list="host1"
pcs stonith create stonith-two fence_ssh user=centos hostname=host2 password=Pa55w0rd sudo=true pcmk_host_list="host2"
pcs constraint location add stonith-one-host-one stonith-one host1 INFINITY
pcs constraint location add stonith-two-host-two stonith-two host2 INFINITY
