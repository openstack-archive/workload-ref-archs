Big Data Sample Heat Template
==============================

This heat templates deploy a Hadoop cluster with Apache Ambari.

Ambari is the central management service for Open Source Hadoop. It provides
central administration and management functionality via a web UI. In this
example, the Ambari service is installed on the MasterNode and an Ambari agent
is deployed on each DataNode in the cluster. This provides communication and
authentication functionality between the Hadoop cluster nodes.

**Type of roles in this Hadoop cluster**

======  ==================================================================
Role    Details
======  ==================================================================
Master  Master Node (aka Name Node) - this node houses the cluster-wide
        management services that provide the internal functionality to manage
        the Hadoop cluster and its resources.
Data    Data Nodes – services used for managing and analyzing the data,
        stored in HDFS, are located on these nodes. Analytics jobs access and
        compute the data on the Data Nodes.
Edge    Services used to access the cluster environment or the data outside
        the cluster are on this node. For security, direct user access to the
        Hadoop cluster should be minimized. Users can access the cluster via
        the command line interface (CLI) from the Edge Node. All data-import
        and data-export processes can be channeled on one or more Edge Nodes.
Admin   Administrative Server - Used for system-wide administration.
======  ==================================================================

This template provision a small testing environment which demonstrate the
deployment of a Hadoop cluster in an OpenStack cloud environment. The
default settings used in this template should not be used without changes
in a production environment. Users are advised to change the settings that
fit in their own environment.

This template was tested using Mitaka & Liberty release of OpenStack.

-----------------
Heat File Details
-----------------
This template requires a few standard components such as an Ubuntu cloud image
and an external network for  internet access.

The template prepares a few resources that are required by the Hadoop
deployment.

Multiple Cinder volumes are created for the Hadoop filesystem.
For simplicity, every node is attached with a Cinder volume with a default size
in this example.

Multiple Neutron subnets are created. This includes:

==================  ======================
Subnet              Details
==================  ======================
Cluster Network     Provides inter-node communication for the Hadoop cluster.
Data Network        Provides a dedicated network for accessing the object
                    storage within an OpenStack Swift environment or to an
                    external object storage such as Amazon S3. This is
                    optional if object storage is not used.
Management Network  Provides a dedicated network for accessing the Hadoop
                    nodes' operating system for maintenance and monitoring
                    purposes.
Edge Network        Provides connectivity to the client-facing and enterprise
                    IT network. End users are accessing the Hadoop cluster
                    through this network.
==================  ======================

Multiple routers are created to route the traffic between subnets.
Other networks can also be created depending on your specific needs.

Security Groups are defined and attached to every Node in the cluster.
Custom rules can be created for different types of nodes to allow/deny
traffic from certain protocols, ports or IP address ranges.

Next, the template creates a few servers of different roles (Master, Data,
Edge, Admin). An Ubuntu 14.04 cloud image is assumed to be used as the default
operating system of each servers.

When the server is booted, additional packages (depending on roles) are
installed and configured on each server. In this example, the Apache Ambari
is installed and all systems are configured with name server, ntp,
package repositories and other necessary settings for the Apache Ambari
service.

The Ambari Web UI can be accessed by pointing to the MasterNode's
IP address at port 8080. A Floating IP can be associated to the MasterNode.

-------------------------------
Running the heat template files
-------------------------------

You need to source the OpenStack credential file. You may download a copy of
the credential file from Horizon under Project>Compute>Access & Security>API
Access

Prior to running the template, please edit and change the default value of each
parameters to the one that match your own environment.

**Example to setup the Hadoop cluster environment**::

  openstack stack create --template BigData.yaml HadoopCluster
