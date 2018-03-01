# fence_ssh
Fencing agent that uses SSH, should only be used for testing.

This is an alternate version of the agent that works using the nodename param that stonith-ng/pacemaker provides to fence machines. This means that you can deploy it on all nodes and not have to specify the hostname.

# How to Use
Place in /usr/sbin with execute permissions

Create stonith resources in Pacemaker

Can see usage with either fence_ssh --help or by running pcs stonith describe fence_ssh

Example usage with PCS:

_Ensure that pcmk_host_list is defined so that Pacemaker knows which resource can fence which node_

pcs stonith create stonith-ssh fence_ssh user=centos password=Pa55w0rd sudo=true pcmk_host_list="host1 host2"

pcs resource clone stonith-ssh clone-max=2 clone-node-max=2
