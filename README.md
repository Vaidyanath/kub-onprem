# kub-onprem

Deploy a fully functional kubernetes infra on bare metal servers
# Prereq

ansible-galaxy install defunctzombie.coreos-bootstrap -p ./roles


# OS
This project is made with CoreOS 962.0.0+ in mind, porting to other OSes
may be doable just keep in mind that you will have to reimplement the
CoreOS's built in stuff like the [kubelet-wrapper](https://coreos.com/kubernetes/docs/latest/kubelet-wrapper.html)

# Logging
A preconfigured Sumo Logic collector is integrated, all you have to do is
to provide a Sumo Logic API Access Key through a kurbenetes secret, the
default secret name is ```sumo-log-api-keys```

To add your keys once the cluster is up :
`kubectl create secret generic sumo-log-api-keys --from-literal=accessid=[yourAccessId] --from-literal=accesskey=[yourAccesskey]`

Your apps/jobs/... will then need to throw all their logs in syslog format
to the collector. The collector will be exposed as a service which will be
reachable inside the pod network, just use the service name as the endpoint
hostname ( the dns part is auto configured by the kube-dns addon )

# Monitoring
See [heapster] and [datadog]

