# NOTES

oc get events --sort-by='.lastTimestamp'

https://komodor.com/learn/how-to-fix-errimagepull-and-**imagepullbackoff**/

The certificate used by the ingress controller operator is a wildcard certificate for all routes in the .apps subdomain for your cluster, such as .apps.ocp4.example.com. Routes for the web console, Grafana, Prometheus, and OAuth use this same wildcard certificate.



OpenShift does not inherit permissions from the LDAP server; permissions must be added to each group.

#openssl x509 -in tls.crt -noout -dates

#oc get events --sort-by='.lastTimestamp' -n openshift-kube-apiserver


Adding your certificates to the **cluster proxy** ensures that your web console pods can trust the authentication pods and vice versa.

The Red Hat OpenShift Container Platform installer creates an **internal certificate authority (CA)** and uses this CA to sign additional certificates.

The certificate used by the **ingress controller operator is a wildcard certificate** for all routes in the .apps subdomain for your cluster, such as .apps.ocp4.example.com. Routes for the webconsole, Grafana, Prometheus, and OAuth use this same wildcard certificate.

The ingress operator configures the ingress controller to route traffic into the OpenShift environment. The certificate used by the ingress controller can be updated so that it uses a
certificate signed by a recognized certificate authority, or by your own enterprise CA. Changing the ingress controller operator to use a different certificate and its associated key only requires a handful of steps. Before starting this process, you need:



The only clients that implicitly trust certificates signed by the internal OpenShift certificate authority are other components within the OpenShift cluster. Therefore,
these certificates should not be replaced.


Navigate to the Discover view, and then click New. Select the app index pattern, and then enter **kubernetes.flat_labels:"app=app1"** in the text field.The results display the total number of log records for the app1 deployment.


#oc whoami -
#oc get deployment/hello -o json | jq '.spec.template.spec.containers[0].image'

Identify the container image specified by the deployment.
oc get deployment/hello -o json | jq '.spec.template.spec.containers[0].image'

Image streams allow administrators to use tags for referencing specific versions of container images.

Source images are stored in image registries, such as registry.redhat.io, or the OpenShift integrated registry. On the contrary, **image streams are virtual references to source images, and **their metadata is stored in etcd.****

**Image streams use a unique SHA256 identifier instead of a mutable image tag.** This approach is more reliable than standard container image tags, such as :latest or :v2.1, where the tagged image can change without notice.

https://access.redhat.com/documentation/en-us/openshift_container_platform/4.12/html-single/cli_tools/index#oc-policy-add-role-to-user

OpenShift builds on Kubernetes and its extensibility, adding features such as **logging, monitoring, and authentication.**

OpenShift Container Platform is a certified Kubernetes distribution

OpenShift provides the oc and kubectl and command-line tools. The oc command adds OpenShift features to the kubectl command.
kubectl and oc in OpenShift are the same binary. The oc binary embeds kubectl code



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

RHEL NFS does not fully support all POSIX locking and caching semantics. Testing
uncovered issues with certain apps using shared storage, such as the internal registry
and HA databases. Therefore, using RHEL NFS to back PVs used by core services is not recommended.


Download and extract the **root CA certificates from vCenter.**
wget vcenter.sddc.vmwaremc.com/downloads/certs/download.zip

vSphere volumes are backed by VMware vSphere Virtual Machine Disk (VMDK) files. Because
vSphere volumes are provided by a traditional virtualization platform, they have the following limitations compared to OpenShift Data Foundation:

Support for **RWO** access mode only
No regional HA or portability
**Incompatible with volume snapshots**
**Vendor lock-in**

The control plane and compute nodes in an OpenShift cluster frequently communicate with each other. **All communication between cluster nodes is protected by mutual authentication
based on per-node TLS certificates.***

All per-node TLS certificates have a short expiration life of 24 hours (the first time) and **30 days** (after renewal).

Proper administration of an OpenShift cluster requires awareness and mitigation of various capacity issues that arise during operation.





