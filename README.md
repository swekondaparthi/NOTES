# NOTES

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
The scheduler uses the value of **node.Status.Allocatabl**e instead of node.Status.**Capacity** to decide if a node will become a candidate for pod scheduling.

