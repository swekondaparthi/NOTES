# NOTES

oc get events -o template --template '{{range .items}}{{.message}}{{"\n"}}{{end}}'

https://medium.com/lumigo/conquering-the-peaks-of-kubernetes-errors-ee2120db50d2

https://github.com/wangzheng422/openshift4-shell/blob/ocp-4.10/operator.sh

https://github.com/openshift/oc-mirror

https://www.redhat.com/sysadmin/openshift-terminating-state

https://ostechnix.com/linux-command-line-tricks/

https://github.com/wangzheng422/docker_env/blob/master/redhat/training/ansible/ansible_host_example

https://cloud.redhat.com/blog/sre-life-helpful-pointers-for-debugging-openshift-1
https://medium.com/@tamber/mini-howto-check-pods-special-scc-needs-before-you-upgrade-to-ocp-4-11-4e23262ae7c
https://medium.com/@tamber/openshift-certificates-101-certificate-expiration-alerting-automation-7f3c280bc4e1
https://medium.com/@tamber/poc-kyverno-policy-reporter-ui-on-openshift-4-x-f79ea6a0818b
https://medium.com/techloop/understanding-kyverno-policies-7e2d8651d7b1

https://medium.com/globant/tracerouting-pod-to-pod-traffic-a45fabd86f77

https://medium.com/@meng.yan/what-happens-when-deleting-a-pod-d1219c7e1b53

https://access.redhat.com/articles/4740011 : Red Hat Operators Supported in Disconnected Mode

https://www.redhat.com/sysadmin/burn-rate-alerts-openshift


https://www.redhat.com/sysadmin/openshift-terminating-state



**How the scheduler determines resource availability**
The scheduler uses the value of **node.Status.Allocatable** instead of node.Status.**Capacity** to decide if a node will become a candidate for pod scheduling.

The problem with ConfigMaps is that we can't store sensitive data. ConfigMaps store the data in plain text or in the format in which we supply the data to the ConfigMaps.

**Kubernetes Secrets**

Kubernetes Secrets when created takes the data and **encodes them into hash using base64** and then stores it in the cluster. Once the secret is created we access the data by mounting them inside the pod or deployment.
Secrets are created using command-line tools like Kubectl and oc commands are called the **Imperative way.**

Encode the sensitive data

echo -n "mysql-db" | base64
echo -n "password" | base64

Secrets separate the sensitive information for the application source code and store it in the cluster at the namespace level


With import_role, the ansible-playbook command starts by parsing and inserting the role in the
play before starting the execution. Ansible detects and reports syntax errors immediately and does
not start the playbook execution.
With include_role, however, Ansible parses and inserts the role in the play when it reaches the
include_role task, during the play execution. If Ansible detects syntax errors in the role, then
execution of the playbook is aborted.

Simple Bash trick to find the **largest file**s on Disk

"find /* -type f -exec du -sh {} + | sort -hr | head -n1


Verify the availability of the **image registry from the cluster nodes**.
curl -kIs https://image-registry.openshift-image-registry.svc:5000/healthz

https://access.redhat.com/articles/6271341

*etcd health*
etcdctl endpoint health --cluster
etcdctl member list -w table
/usr/local/bin/cluster-backup.sh

Although etcd is not particularly I/O intensive, it requires a low latency block device for optimal performance and stability. Because etcd’s consensus protocol depends on persistently storing metadata to a log (WAL), etcd is sensitive to disk-write latency. Slow disks and disk activity from other processes can cause long fsync latencies.

Run etcd on machines that are backed by SSD or NVMe disks with low latency and high throughput.

The load on etcd arises from static factors, such as the number of nodes and pods, and dynamic factors, including changes in endpoints due to pod autoscaling, pod restarts, job executions, and other workload-related events

History compaction is performed automatically every five minutes and leaves gaps in the back-end database. This fragmented space is available for use by etcd, but is not available to the host file system. You must defragment etcd to make this space available to the host file system.

Defragmentation occurs automatically, but you can also trigger it manually.

The default etcd space quota size is approximately 7.5 GB, and is defined by the variable etcd_server_quota_backend_bytes. If an etcd database exceeds this quota, you
must defragment and compact it.
etcd_server_quota_backend_bytes

An etcd backup contains the status of the cluster and the configuration of the static pods running on a control plane node

oc get pods --all-namespaces | grep -v -E 'Running|Completed'
chronyc tracking

Verify that the **three etcd members** are available to the OpenShift cluster.
oc get etcd -o=jsonpath='{range .items[0].status.conditions[?(@.type=="EtcdMembersAvailable")]}{.message}{"\n"}'

oc get csr -o go-template='{{range .items}}{{if not .status}}{{.metadata.name}}{{"\n"}}{{end}}{{end}}' | xargs oc adm certificate approve



**Installing** an OpenShift Cluster on **vSphere** with Pre-existing Infrastructure.

Download the installer binary, oc tools, and pull secret from the Red Hat OpenShift Cluster Manager site.
Download the root CA certificates for vCenter and add them to your bastion VM.
Download the bare metal install image.
Verify DNS, HAproxy, and Apache Web server configurations.
Manually create the install-config.yaml file.
Create the manifest files.
Modify the manifest/cluster-schedular-02 file to reflect uppercase False.
Create the ignition files.
Make the ignition files available via HTTPD.
Create append-bootstrap.ign to point to the URL for bootstrap.ign.
Convert the ignition files using base64 encoding.
Download the RHCOS.ova file and deploy the template.
Clone the template to create cluster VMs.
Add base64 encoding of ignition files to the corresponding VMs.
Power on the VM and pass kernel line arguments to customize the cluster VMs.
Use the openshift-install binary to monitor the bootstrapping process.
Remove the bootstrap entry from the load balancer after bootstrapping completes.
Use the openshift-install binary to monitor the deployment progress until completion. 

Usage of port 22623 in OpenShift 4 api-int : https://access.redhat.com/solutions/4926401

**MCP:**
https://www.redhat.com/en/blog/openshift-container-platform-4-how-does-machine-config-pool-work

api-int.<cluster_name>.<base_domain>: VIP3
The DNS records must be resolvable from all the nodes within the cluster.

![image](https://github.com/swekondaparthi/NOTES/assets/8417059/d4073f36-40ee-47cf-85b9-352dd4b143e7)


