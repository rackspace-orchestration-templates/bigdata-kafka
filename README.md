Description
==========

This is a Heat template to deploy a Rackspace Cloud Big Data cluster.

Requirements
==========
* [python-heatclient](https://github.com/openstack/python-heatclient) `>= v0.2.8`:

```bash
pip install python-heatclient
```
* An Rackspace username, password, and tenant id.

We recommend installing the client within a [Python virtual
environment](http://www.virtualenv.org/).

Example Usage
=============
Here is an example of how to deploy this template using the
[python-heatclient](https://github.com/openstack/python-heatclient):

More CLI examples can be found in [README](https://github.com/rackerlabs/cbd_heat_plugin/blob/master/README.md)
##### Create a Heat Stack
```sh
heat --os-region-name <REGION> --os-auth-url https://identity.api.rackspacecloud.com/v2.0/ --os-tenant-id <TENANT-ID> --os-username <OS-USERNAME> --os-password <OS-PASSWORD> stack-create -f hadoop.yaml <CLUSTER-NAME>
```
Optionally, set environmental variables to avoid needing to provide these values every time a call is made:

```
export OS_USERNAME=<USERNAME>
export OS_PASSWORD=<PASSWORD>
export OS_TENANT_ID=<TENANT-ID>
export OS_AUTH_URL=<AUTH-URL>
```

Parameters
=========
Parameters can be replaced with your own values when standing up a stack.

 - `stackId`: A "stack" is a predefined cluster topology provided by the Cloud Big Data 
 product.  This is the ID for one of those stacks, i.e. HADOOP_HDP2_3.  To get a current list of 
 available stacks, refer to the API documentation. 
 - `clusterName`: A descriptive name of the cluster; useful when you have multiple clusters.
 - `clusterLogin`: The system username to be used for getting access to the cluster.  You can 
 use this to log in to individual servers using SSH, and run commands against your cluster.
 Example: ssh <clusterLogin>@<server IP>
 - `flavor`: The flavor defines the resources (like disk space and RAM) available on the 
 slave nodes in the cluster. Flavors are updated when new cloud hardware is 
 available so it is always best to check the CBD REST API for the current list (see Reference 
 Documentation below for details).
 - `numSlaveNodes`: numSlaveNodes is the number of servers in the cluster that perform slave roles 
 like DataNode for HDFS or NodeManager for YARN.  These nodes are where data replicas live as 
 well as where tasks are executed.  3 is a useful minimum, as that gives you at least 2 copies of
  your data.
 - `publicKeyName`: publicKeyName is an easy to remember name for the SSH public key used in the 
 cluster. This name may be reused in other clusters in order to reuse public keys and allow the 
 same private key to SSH into clusters across a company/organization if desired.
 - `publicKey` This is the full public key (matching your securely stored private key) that will be 
 installed into the cluster systems which enable SSHing into cluster nodes. CBD clusters disable 
 login/password-based SSH connections so this key is required for cluster access. It is important 
 to put quotes around this value.

Outputs
=======

Once a stack comes online, use `heat output-list` to see all available outputs.
Use `heat output-show <OUTPUT NAME>` to get the value for a specific output.
 
 * `cluster_id`:  Cloud big data cluster ID.
 * `cbd_version`: Current cloud big data version used.
 
Contributing
============
There are substantial changes still happening within the [OpenStack
Heat](https://wiki.openstack.org/wiki/Heat) project. Template contribution
guidelines will be drafted in the near future.

License
=======
```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```


