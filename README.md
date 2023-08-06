# NOTES

https://medium.com/lumigo/conquering-the-peaks-of-kubernetes-errors-ee2120db50d2

https://github.com/wangzheng422/openshift4-shell/blob/ocp-4.10/operator.sh

https://github.com/openshift/oc-mirror

https://ostechnix.com/linux-command-line-tricks/

https://github.com/wangzheng422/docker_env/blob/master/redhat/training/ansible/ansible_host_example

https://cloud.redhat.com/blog/sre-life-helpful-pointers-for-debugging-openshift-1
https://medium.com/@tamber/mini-howto-check-pods-special-scc-needs-before-you-upgrade-to-ocp-4-11-4e23262ae7c
https://medium.com/@tamber/openshift-certificates-101-certificate-expiration-alerting-automation-7f3c280bc4e1
https://medium.com/@tamber/poc-kyverno-policy-reporter-ui-on-openshift-4-x-f79ea6a0818b
https://medium.com/techloop/understanding-kyverno-policies-7e2d8651d7b1

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


