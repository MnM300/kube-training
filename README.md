# kube-training
Devops training 

WELCOME TO DevOps Tools - Git, CKAD, AKS, Jenkins and GitLab


Trainer name: Shruti Kulshrestha 
Trainer contact email address: shruti.kulshreshta@koenig-solutions.com
Trainer contact info: +91-868186187
                                     +971-547147710 

Table Of Content: https://rms.koenig-solutions.com/Sync_data/Forms/CRM/Files/Freelancer/2021928210-DevOpsTools.pdf

Documentation:
    presentation: AI AND MANUAL (KUBERNETES)
    LAB GUIDE : AI
    COURSEBOOK : AI 
    etherpad notes: handy notes 
    
   
    

•START TIME        :  9:00AM 
•SNACK TIME       :  10:00PM -10:15PM (15MINS )
•LUNCH BREAK    :  12:00PM -1:00PM
•SNACK TIME       :  3:30PM -3:50PM   (20MINS)
•END TIME            :   4:30PM

=================================================================================

BASIC LINUX: DONE

INSTALLATION ON ON-PREMISES AND AKS (CLOUD)  AND KIND OR MINIKUBE 

LAB CREDITINALS 

url :  portal.azure.com


For Georges
shruti02@abhisoni01011992hotmail.onmicrosoft.com
Fuku@Train0506!

For joel 
shruti03@abhisoni01011992hotmail.onmicrosoft.com
Vuqu@Koenig2027

For Rondy
shruti04@abhisoni01011992hotmail.onmicrosoft.com
Waga2407


student06@abhisoni01011992hotmail.onmicrosoft.com
@8368186187sK

    
    
    
Joel Dupres                               
apr27ri-alwanew                     
Pa$$w0rdPp
https://linuxlab.koenig-solutions.com


Georges Esparon
apr27nz-alwanew
Pa$$w0rds[
    https://linuxlab.koenig-solutions.com Password

Rondy Monnaine
apr27jr-alwanew
Pa$$w0rdR#
https://linuxlab.koenig-solutions.com/

for koenig dc 
student user 
password: student 


root user:
password: redhat 

vim editor operations

to write in the vim editor:
 press esc + i

to save  file and quit
esc
shift+:
wq

w= save
q= quit
!= forcefulexit


 undo the changes
press esc
shift+:
u


copy and paste : yanking
take cursor from wheere u wish to copy
press esc
3 yy
take cursor where u wish to paste it
press p


to  delete  the lines
press esc
4 dd


---------------------------------
draw.io 

offical site for cncf : https://landscape.cncf.io/
Basic Commands
# kubectl get nodes                        -> to list all nodes
# kubectl get nodes -o wide                -> list nodes with more info
# kubectl get nodes worker1 -o wide        -> get specific node with more info
# kubectl describe nodes                   -> get detailed information about all nodes
# kubectl describe nodes worker1           -> get detailed info about specific node

Creating Kubernetes Resources 

Deploying Pods with commands 

# kubectl --help                                             -> to get help about the command 
# kubectl get pods                                           -> list pods in current namespace
# kubectl run mypod --image=nginx            -> create new pod
kubectl run pod2  --image=redis 
kubectl run pod2  --image=quay.io/shruti1988/webapp
# kubectl get pods                                           -> list pods
# kubectl get pods mypod                                     -> get specific pod
# kubectl get pods -o wide                                   -> get more info on all pods
# kubectl get pods mypod -o wide                             -> get more info on specific pod
# kubectl describe pods                                      -> get detailed info on all pods
# kubectl describe pod mypod                                 -> get detailed info on specific pod
kubectl delete pod pod2 pod3 

==============================================================================================================================
DAY2:
MCQ QUESTIONS: QUBITS :    https://www.qubits42.com/live/57369


TOPIC FOR DAY2

Managing Pods Managing Labels & Selector
Managing Replication Controller & Replica Set 
Managing Service 


INSTALLATION OF KUBERNeTES  CLUSTER 

Step1: Install the CRE  (i,e cri-o)

open the website in the web-broswer    https://cri-o.io/



Define the Kubernetes version and used CRI-O stream
KUBERNETES_VERSION=v1.32CRIO_VERSION=v1.32   (  on master  and node1 and node2)


Distributions using rpm packagesAdd the Kubernetes repository (  on master  and node1 and node2)
cat <<EOF | tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/$KUBERNETES_VERSION/rpm/repodata/repomd.xml.keyEOF


Add the CRI-O repository    (  on master  and node1 and node2)
cat <<EOF | tee /etc/yum.repos.d/cri-o.repo
[cri-o]
name=CRI-O
baseurl=https://download.opensuse.org/repositories/isv:/cri-o:/stable:/$CRIO_VERSION/rpm/
enabled=1
gpgcheck=1
gpgkey=https://download.opensuse.org/repositories/isv:/cri-o:/stable:/$CRIO_VERSION/rpm/repodata/repomd.xml.keyEOF

 

Install package dependencies from the official repositories  (  on master  and node1 and node2)
dnf install -y container-selinux


Install the packages (  on master  and node1 and node2)
dnf install -y cri-o kubelet kubeadm kubectl

Start CRI-O (  on master  and node1 and node2)
systemctl start crio.service


Bootstrap a cluster  (  on master  and node1 and node2)
swapoff -a
modprobe br_netfilter
sysctl -w net.ipv4.ip_forward=1


EXECUTE THE COMMAND TO INITIALISE THE CLUSTER (  on master  )

kubeadm init --pod-network-cidr=10.244.0.0/16
export KUBECONFIG=/etc/kubernetes/admin.conf

vim /root/.bashrc
   export KUBECONFIG=/etc/kubernetes/admin.conf   ( copy and paster this command in the bashrc file)
kubectl get nodes

Join the Cluster -> on ALL Worker nodes
# kubeadm join 172.25.232.87:6443 --token 1dv3i8.ekfgu01i5ue7s80o \
    --discovery-token-ca-cert-hash sha256:8132dfdbd09ecacbbd4d8615a8fe8de1d11d7739b7be3cafef92768cf7bc5937
    (note: check the command from kubeadm init command output)

If you want to create new token along with print command then run below command on the master node then copy the output and paste on to the workers
# kubeadm token create --print-join-command



Network solutions (Calico)
 https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/onpremises#install-calico-with-kubernetes-api-datastore-50-nodes-or-less
curl https://raw.githubusercontent.com/projectcalico/calico/v3.30.3/manifests/calico.yaml -O

# gedit calico.yaml
Note: find docker.io and replace it with quay.io

# kubectl apply -f calico.yaml
# watch kubectl get pod -A  -> Once all the pods start running presss Ctrl + C
# kubectl get nodes

Bash Autocompletion
# kubectl completion bash > .kube/kube.sh
# source .kube/kube.sh
# gedit .bashrc
source /root/.kube/kube.sh


===============================================================

how to write the yaml structure

-  grandfather 
    -  robin 
        -   robin son 
        -    robin daughter
    - batman
       -  batman son 
       - batman daughter
- grandfather brother 



english ,  indentation 

extension: .yaml , .yml


*************************************************************************************************
SHORTCUTS
alias k=kubectl 

for indentation:---
===========
vim   .vimrc

set ai                                             (set auto indentation)
set nu                                             ( set autonumber)
set cursorcolumn              
set ts= 2                                          ( set tab space=2)
set et                                                (expand tab)

CTRL+a === will go at the start of the command 
ctrl+e  ==will go at the end of command line
atl+.  == copy the last arugument
ctrl+l == clear the screen 

=============================================================
DEMO2: TO CREATE MULTI-CONTAINER POD

FILENAME:   vim pod3-multicontainer.yaml

apiVersion: v1
kind: Pod
metadata:
 name: pod4
spec:
 containers:
 - name: cont1
   image: nginx
 - name: cont2
   image: memcached
 - name: cont3
   image: redis
   
   kubectl apply -f pod3-multicontainer.yml
   kubectl get pods -o wide
   kubectl describe pod multi-pod
   
   kubectcl exec -it multi-pod .yml
   kubectl exec -it pod4 -c c1  -- bash  OR   kubectl exec -it pod4 -c c1 -- /bin/bash 
    kubectl exec -it pod4  -c c2  --  bash
    kubectl exec -it pod4  -c c3  --  bash


IMAGEPULLPOLICY

 imagePullPolicy tells Kubernetes when to pull (download) the container image from a registry.
 
 ALWAYS: Kubernetes will always pull the image from the registry every time a Pod starts.
 IFNOTPRESENT:  Kubernetes will pull the image only if it is NOT found on the node.
 NEVER: Kubernetes will never pull the image from the registry, even if it is not present locally.
If the image is missing on the node → Pod will fail.
 
 DEMO3: FILENAME:  vim pullpolicypod.yaml 
 
apiVersion: v1
kind: Pod
metadata:
  name: pod5
spec:
  containers:
  - name: cont1
    image: nginx
    imagePullPolicy: IfNotPresent
   
   
   kubectl apply -f  pullpolicypod.yaml
   kubectl get pods -o wide  
==============================================================
LABELS
Labels are key-value pairs attached to Kubernetes objects such as Pods, Deployments, Services, Nodes, etc.They help identify, organize, and group resources in Kubernetes.

THROUGH IMPERATIVE WAY  LABELLING THE EXITING PODS 
kubectl  label  pod pod5 tier=frontend 
k get pods -o wide --show -labels 
k label  pod pod1 tier=frontend env=prod backup=weekly 
k get pods -o wide --show-labels 
k label  pod pod2 tier=frontend env=dev backup=weekly 
k label  pod pod3 tier=backend env=dev backup=weekly 
k label  pod pod4 tier=backend env=testing backup=weekly 
k get pods -o wide --show-labels 

RUNNING THE POD AND LABELLING IT THROUGH IMPERATIVE WAY
k run pod6 --image=nginx  --labels="env=prod"
k get pods -o wide --show-labels 

DELETING THE LABELS ON THE POD
k label pod pod4 backup-
k get pods -o wide --show-labels 
  
OVERWRITING THE POD
k label pod pod4 --overwrite env=staging
k get pods -o wide --show-labels 

DEMO4: LABELS DELCARATIVE WAY

FILENAME:  vim label.yaml  

apiVersion: v1
kind: Pod
metadata:
  name: label-hello
  labels:
    app: ola
    tier: backend
    env: staging
spec:
  containers:
  - name: cont1
    image: nginx
                                                                                                                                              
 k apply -f label.yaml
k get pods -o wide --show-labels 
  
  
  
   SELECTOR  
A selector is a way to match Kubernetes objects using labels.
Selectors allow controllers (like Services, Deployments, ReplicaSets, etc.) to find and control the right Pods.


Types
      a> equity/equality based selector----
         ------> it will work on single key with single value.
         ------->Equality-based selectors match labels using exact comparisons.
DEMO5:  ON SELECTOR 
        ======
        
        
kubectl  get pods --selector tier=frontend
kubectl get pods --selector env=prod
kubectl  get pods -l env=testing
kubectl  get pods -l env=testing --show-labels 
kubectl  get pods -l env!=testing --show-labels             (!=not equal to) 
                               
                               
      b> set based selector-----
      Set-based selectors allow matching multiple values, not just one.
       They treat label values like items in a set.
                       ----------> it will work on single key with multiple values
                       ----------> it has two types operator
                       
                       a> in   ----------- equal to operator
                       b> notin --------> not equal to operator
                       
# kubetl  get pods --selector 'tier in (frontend, backend)'
# kubectl  get pods --selector 'tier in (frontend,backend)' --show-labels 
# kubectl  get pods --selector 'tier notin (frontend,backend)' --show-labels 
 

#kubectl get pods --selector 'env in (testing,dev),tier in (backend,frontend)' --show-labels
#kubectl get pods --selector 'env in (testing,dev),tier notin (backend,frontend)' --show-labels


===================================================================================================================



 REPLICATION CONTROLLER (rc)
 A Replication Controller (RC) is a Kubernetes object that ensures a specified number of Pod replicas are always running.It is an older Kubernetes workload controller (now largely replaced by ReplicaSets), but still important to understand.

✅ Main Purpose of a Replication Controller
Maintain desired number of pods
If a Pod crashes → RC creates a new one
If a Pod is deleted manually → RC replaces it
If a Pod is extra (more than desired) → RC deletes it
Provide high availability
Ensures your application always has enough running Pods
Enable scaling
Increase or decrease replicas easily
  

kubectl explain rc | less
DEMO6:  
FILENAME :  vim rc.yaml 

apiVersion: v1
kind: ReplicationController
metadata:
  name: rc-web
spec:    
  replicas: 5
  selector:
    app: nginx 
  template:
    metadata:
      name: web
      labels:
        app: nginx
    spec:
      containers:
      - name: web
        image: quay.io/shruti1988/webapp

kubectl apply -f rc.yml 
kubectl get rc -o wide
kubectl get pods
 kubectl delete pod myreplica-w5zl8
 kubectl get rc
 
 scale of apps:--
==========
(manual scaling)
# kubectl scale rc rc-web --replicas 10

  
for schedule maintenence:---
======================
# kubectl  cordon worker2
# kubectl drain worker2 --delete-emptydir-data --ignore-daemonsets --force 

now do all the schedule maintenence

when manitenence will be over:--
kubectl  uncordon worker2

TO DELETE THE REPLICATION CONTROLLER
# kubectl  delete rc rc-web 
=============================================================================================================


DAY3: 
    QUBITS :    https://www.qubits42.com/live/57382
    
    
    
    REPLICASETS
  
=============================================================================================================
REPLICATION SET (RS)

A ReplicaSet (RS) is a Kubernetes workload resource that ensures a specified number of identical Pods are always running.It is the newer and improved version of Replication Controller.
✅ Main Purpose of a ReplicaSet
Maintain desired number of Pods
If a Pod crashes → RS creates a new one
If a Pod is deleted → RS automatically replaces it
If more Pods than required exist → RS deletes extras
Support advanced label selectors
Unlike RC, ReplicaSets support set-based selectors
Scale applications easily
Increase or decrease replicas with simple commands



labs:--
     DEMO7 :  (rs with equity based selector)
     =======================
kubectl  get replicasets.apps 
kubectl  get rs

apiVersion: apps/v1
kind: ReplicaSet
metadata:   
 name: myreplica  
spec:       
 replicas: 6
 selector:  
  matchLabels:
    release: alpha
 template:  
  metadata: 
   labels:  
     release: alpha          
  spec:     
   containers:
   - name: xyz
    image: quay.io/shruti1988/webapp
    imagePullPolicy: IfNotPresent


kubectl  get rs -o wide

scale of apps:--
==========
(manual scaling)
# kubectl scale rs myreplica --replicas 10


for schedule maintenence:---
======================
# kubectl  cordon worker2
# kubectl drain worker2 --delete-emptydir-data --ignore-daemonsets --force 

now do all the schedule maintenence

when manitenence will be over:--
# kubectl  uncordon worker2

TO DELETE THE REPLICATION CONTROLLER
# kubectl  delete rs myreplica 



DEMO8: rs with set based selector:---
=======================

filename: vim rs-equity.yaml

apiVersion: apps/v1                
kind: ReplicaSet                   
metadata:                          
 name: setrs                       
spec:                              
 replicas: 6                       
 selector:                         
  matchExpressions:                
  - key: app                     
    operator: In                   
    values:                        
    - app1                     
    - app2                    
 template:                         
  metadata:                        
   labels:                         
      app: app1               
  spec:                            
   containers:                     
   - name: xyz                     
     image: quay.io/shruti1988/webapp
     imagePullPolicy: IfNotPresent
     
kubectl apply -f rs-equity.yaml
k get rs 
k get rs -o wide
k get pods -o wide

================================================================================================================================

DAEMONSET(ds)

A DaemonSet ensures that one Pod (or more) runs on every node in the Kubernetes cluster—or on specific selected nodes.
Think of it as:
“Run this Pod on all nodes automatically.”

Why Do We Use DaemonSets?
DaemonSets are used for node-level services, such as:
🔹 1. Monitoring Agents
Prometheus Node Exporter
Datadog agent
New Relic agent
 2. Logging Agents
Fluentd
Logstash
Filebeat
🔹 3. Networking Components
CNI plugins
kube-proxy
Calico / Weave / Flannel agents
🔹 4. Storage Daemons
Ceph
GlusterFS

 DAEMONSET


apiVersion: apps/v1                         
kind: DaemonSet                             
metadata:                                   
 name: myds                                 
spec:                                       
 selector:                                  
  matchLabels:                              
   release: beta                         
 template:                                  
  metadata:                                 
   labels:                                  
    release: beta                       
  spec:                                     
   containers:                              
   - name: xyz                              
     image: nginx
     imagePullPolicy: IfNotPresent

# kubectl  get daemonsets.apps 
# kubectl  get ds     
k get pods -o wide


==================================================================================================

SERVICE

A Service in Kubernetes is an object that provides stable networking for Pods.
It ensures reliable communication even when Pods change, restart, or move.
Think of a Service as:
A permanent IP + DNS name for a group of Pods.
-   cluster IP
-   NODEPORT
-  LOADBALANCER


DEMO10:  CLUSTER IP
 
apiVersion: v1 
kind: Service  
metadata:      
 name: clusterip  
spec:          
 type: ClusterIP
 ports:        
 - port: 6500  
   targetPort: 80
 selector:     
    app: nginx

k apply -f <filename.yaml>
k get svc 
k get svc -o wide


web-broswer: copy the clusterip :6500



[root@master ~]# k get svc -o wide
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE   SELECTOR
clusterip-1   ClusterIP   10.98.72.121   <none>        6500/TCP   38s   app=nginx
kubernetes    ClusterIP   10.96.0.1      <none>        443/TCP    24h   <none>

DEMO11: NODEPORT SERVICE

apiVersion: v1 
kind: Service  
metadata:      
 name: mysvc2  
spec:          
 type: NodePort
 ports:        
 - port: 6501  
   targetPort: 80
   nodePort: 30000
 selector:     
   app:nginx
 kubectl  get svc -o wide

k apply -f <filename.yaml>
k get svc 


[root@master ~]# k get svc -o wide
NAME          TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE     SELECTOR
clusterip-1   ClusterIP   10.98.72.121   <none>        6500/TCP         21m     app=nginx
kubernetes    ClusterIP   10.96.0.1      <none>        443/TCP          24h     <none>
nodeport-1    NodePort    10.99.247.98   <none>        6501:30000/TCP   8m18s   release=alpha




cross-verify 

web-broswer: copy the clusterip :6501
check the ip address of host machine by command ip addr
hostmachine ip:30000



DEMO12  : LOAD BALANCER

step-1
install loadbalancer (metallb):---
=====================
google----> install metallb in kubernnetes
# wget https://raw.githubusercontent.com/metallb/metallb/v0.13.10/config/manifests/metallb-native.yaml
# kubectl  apply -f  metallb-native.yaml 
# kubectl  get ns    ------> to see new ns  "metallb-system"
# kubectl  get pods -n metallb-system 

step-2
======
create ipaddresspool for metallb loadbalancer :---
=================================
# kubectl  get ipaddresspool
# kubectl  get ipaddresspools.metallb.io -n metallb-system 

filename: vim ipaddresspool.yaml

apiVersion: metallb.io/v1beta1  
kind: IPAddressPool             
metadata:                       
  name: first-pool              
  namespace: metallb-system     
spec:                           
  addresses:                    
  - 172.25.230.10-172.25.230.20
  
  kubectl apply -f <filename>.yaml
  kubectl get ipaddresspool -n metallb-system   (cross-verify)  
  
==========================================  
  STEP:3


apiVersion: v1
kind: Service
metadata:
 name: loadsvc3
spec:
 type: LoadBalancer
 loadBalancerIP: 172.25.230.20
 ports:
 - port: 80
   targetPort: 80
 selector:
  app: app1

k apply -f <filename.yaml>
k get svc 
k get svc -o wide

web-broswer: copy the loadbalancer

==================================================================================================================

NAMESPACE
k create ns prod 
  363  k get ns 
  364  k run pod1 --image=quay.io/shruti1988/webapp -n prod 
  365  k run pod1-cbs --image=quay.io/shruti1988/webapp -n prod 
  366  k get pods 
  367  k get pods -n prod 
  368  k get pods 
  369  kubectl get pods -A 


[root@master ~]# vim rc.yaml
[root@master ~]# k apply -f rc.yaml  -n dev
replicationcontroller/rc-web created
[root@master ~]# k get pods -n dev
NAME           READY   STATUS              RESTARTS   AGE
rc-web-888pk   1/1     Running             0          8s
rc-web-9xwmx   1/1     Running             0          8s
rc-web-hl2tr   1/1     Running             0          8s
rc-web-jkzfr   0/1     ContainerCreating   0          8s
rc-web-v75jd   1/1     Running             0          8s


Namespace/ns:----
===========
              ----------> these are  logical clusters  on the top of physical k8s cluster
              -----------> it helps to isolate/seperate k8s resources from one ns to another ns
    
  CREATING NAMESPACE
# kubectl  get namespaces 
# kubectl  get ns
# kubectl get pods -A 
# kubectl get all    -----> to see all the resources in default ns
# kubectl get all -n kube-system 

how to create new ns:--
===================
apiVersion: v1 
kind: Namespace
metadata:  
 name: prod


# kubectl  create ns dev

      how to create resource in a ns:---
=========================
apiVersion: v1
kind: Namespace
metadata:
 name:  testing
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:   
 name: myreplica  
 namespace: testing 
spec:       
 replicas: 6
 selector:  
  matchLabels:
    release: alpha
 template:  
  metadata: 
   labels:  
     release: alpha          
  spec:     
   containers:
   - name: xyz
    image: quay.io/shruti1988/webapp
    imagePullPolicy: IfNotPresent 

     
     k apply -f filename.yaml
     k get deployment -o wide
     
---
apiVersion: v1
kind: Service
metadata:
 name: my-svc1
 namespace: testing
spec:
 type: LoadBalancer
 loadBalancerIP: 172.25.230.17
 ports:
 - port: 80
   targetPort: 80
 selector:
    app: java

k apply -f filename.yaml
 k get svc -o wide
 copy loadbaalancer id    

MANUAL SCHEDULING 
vim <filename.yaml>

apiVersion: v1          
kind: Pod               
metadata:               
 name: manual-pod       
spec:                   
  containers:           
  - name: xyz           
    image: quay.io/shruti1988/webapp
    imagePullPolicy: IfNotPresent
  nodeName: node2
  
  k apply -f filename.yaml
  k get pods -o wide ( check the node namewhere pod got created) 
  
DEMO18:  MANUAL SCHEDULING (labeling the node)
  
 (nodeSelector-------- create pod on the basis of node label)
  
  # kubectl  get nodes --show-labels 
  # kubectl label nodes node2  disk=ssd
   # kubectl  get nodes --show-labels 

to delete the label on node
# kubectl label nodes worker2 disk-

vim <filename>.yaml

apiVersion: v1
kind: Pod     
metadata:     
 name: node-pod                 
spec:         
 containers:  
 - name: xyz  
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent
 nodeSelector:
  disk: ssd
---------------------------------------------------------------------------------------------------
Taint & Tolerations
Taints and tolerations work together to control which pods can run on which nodes.
Think of it like this:
Taint = “Keep pods away from me unless they have permission.”
Toleration = “I have permission to run on that tainted node.”

Effect                                           Meaning
NoSchedule                               Pod will NOT be scheduled unless it has a toleration
PreferNoSchedule                    Try not to schedule, but allowed if needed
NoExecute                                  Evicts pods that don’t tolerate the taint

DEMO19: (  CONDITION: NOEXECUTE)

kubectl  describe nodes node1| less
kubectl  describe nodes node1 |grep -i taints
# kubectl  taint node node1 game=cricket:NoExecute
# kubectl  taint node node1 game=cricket :NoExecute   

# kubectl  taint node worker1 game-    ------> to remove/delete taints value 

vim <filename>.yaml

apiVersion: v1         
kind: Pod              
metadata:          
 name: toleration-pod         
spec:                  
 containers:           
 - name: xyz           
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent
 tolerations:          
 - key: "game"         
   operator: "Equal"   
   value: "cricket"     
   effect: "NoExecute"


DEMO19: (  CONDITION: NOSCHEDULE)
kubectl taint node node1 app=web:NoSchedule

 vim taint.yml 

apiVersion: v1
kind: Pod
metadata:
  name: my-web
spec:
 containers:
 - name: c1
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent
 tolerations:
 - key: "app"
   operator: "Equal"
   value: "web"
   effect: "NoSchedule"

# kubectl create -f taint.yml
# kubectl get pods my-web -o wide
# kubectl get pods -o wide


================================================================================================================================apiVersio 

remember to label the node

vim affinity.yml 
apiVersion: v1
kind: Pod
metadata:
 name:  affinity-pod
spec:
 containers:
 - name: c1
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent
 affinity:
  nodeAffinity:
   requiredDuringSchedulingIgnoredDuringExecution:
    nodeSelectorTerms:
    - matchExpressions:
      - key: "size"
        operator: "In"
        values:
        - "large"
        - "medium"


# kubectl taint node worker1 app-        
# kubectl create -f affinity.yml
# kubectl get pods -o wide 

Example:21
This affinity rule tells Kubernetes:
👉 Do NOT schedule the pod on nodes where size=small.
👉 The pod can run on any other node (medium, large, or nodes without the size label).


# vim affinity.yml 

apiVersion: v1
kind: Pod
metadata:
 name: my-web3
spec:
 containers:
 - name: c1
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent
 affinity:
  nodeAffinity:
   perrerredDuringSchedulingIgnoredDuringExecution:
    nodeSelectorTerms:
    - matchExpressions:
      - key: "size"
        operator: "In"
        values:
        - "small"

# kubectl create -f affinity.yml
# kubectl get pods -o wide 
=========================================================================================================
Day4 

TASK1:
    
    1. create a Kubernetes ReplicaSet called web-app with 4 replicas, ensuring that each Pod has the label app=nginxserver. After that, expose the ReplicaSet using a Service of type LoadBalancer to make the application accessible externally.
    
       2.  Schedule a Pod manually on node2 and apply the label capacity=highcpu to the node for identification and resource classification.
====================================================================================================================================
 

Deployments

DEPLOYMENT 
A Rolling Deployment is a Kubernetes deployment strategy that updates your application gradually, replacing old pods with new pods one by one or in small batches — without downtime.
✅ How Rolling Deployment Works
You already have some old version pods running.
When you apply a new Deployment version (kubectl apply -f deploy.yaml):
Kubernetes creates new version pods.
Slowly removes the old version pods.
At any point:
Some pods run old version
Some run new version
(until the rollout completes)
This ensures:
✔ Application stays available
✔ No downtime
✔ Safe transition

EXTRA KNOWLEDGE : 
maxUnavailable   :How many pods can be down during update (default: 25%)
maxSurge :How many extra pods can be created above the desired count (default: 25%)


DEMO13: DEPLOYMENT (BY DEFAULT ROLLING TYPE)
vim <filename>.yaml

apiVersion: apps/v1                              
kind: Deployment                                 
metadata:                                        
 name: deploy-rolling                                
spec:                                            
 replicas: 6                                     
 selector:                                       
  matchLabels:                                   
    env: production                           
 template:                                       
  metadata:                                      
   labels:                                       
   env: production                             
  spec:                                          
   containers:                                   
   - name: test                                  
     image: quay.io/shruti1988/production:v1
     imagePullPolicy: IfNotPresent


k apply -f <filename>.yaml
k get deployment
k get deployments.apps
k get deployment -o wide

step-2
configure service:---
===============
# kubectl  expose deployment   deploy-rolling  --port 80 --target-port 80 --name rolling-svc  --type LoadBalancer
k get svc -o wide
copy the load balancer ip adress and paste in broswer (keep refreshering the page)


step-3
application versioning/upgradation:---
================================
# kubectl set image deployment deploy-rolling test=quay.io/shruti1988/production:v2  --record
# kubectl set image deployment deploy-rolling test=quay.io/shruti1988/production:v3  --record
# kubectl set image deployment deploy-rolling test=quay.io/shruti1988/production:v4 --record
# kubectl set image deployment deploy-rolling test=quay.io/shruti1988/production:v5  --record

                      
step-4
how to check the version history:---

#kubectl  rollout history deployment deploy-rolling
remember : to check the revision version 

step-5
======================================================
(roll back of appps)

# kubectl rollout undo deployment deploy-rolling    ----- for 1 step back/rollout
# kubectl rollout undo deployment deploy-rolling --to-revision 2   ----> rollback for  a specific version


step-6
scaling of apps:---
===================
# kubectl scale deployment deploy-rolling --replicas 10
deployment.apps/deploy-rolling scaled

=========================================================================================
DEMO14  : DEPLOYMENT (RECREATE )
====================================================================================================
implement deployment strategy Recreate:---

vim <filename.yaml>

apiVersion: apps/v1               
kind: Deployment
metadata: 
 name: deploy-recreate 
spec:     
 strategy:      
  type: Recreate
 replicas: 6    
 selector:
  matchLabels:  
   app: linuxL 
 template:
  metadata:     
   labels:
      app: linux  
  spec:   
   containers:  
   - name: test  
     image: quay.io/shruti1988/production:v1
     imagePullPolicy: IfNotPresent
     
 k apply -f <filename>.yaml
k get deployment
k get deployments.apps
k get deployment -o wide
k get pods -o wide

step-2
configure service:---
===============
# kubectl  expose deployment   deploy-recreate   --port 80 --target-port 80 --name recreate-svc  --type LoadBalancer
k get svc -o wide
copy the load balancer ip adress and paste in broswer (keep refreshering the page)


step-3
application versioning/upgradation:---
================================
# kubectl set image deployment deploy-recreate test=quay.io/shruti1988/production:v2  --record
# kubectl set image deployment deploy-recreatetest=quay.io/shruti1988/production:v3  --record
# kubectl set image deployment deploy-recreate test=quay.io/shruti1988/production:v4 --record
# kubectl set image deployment deploy-recreate test=quay.io/shruti1988/production:v5  --record

                      
step-4
how to check the version history:---
# kubectl  rollout history deployment deploy-recreate

remember : to check the revision version 

step-5
=====

# kubectl rollout undo deployment deploy--recreate    ----- for 1 step back/rollout
kubectl annotate deployment myapp-deployment kubernetes.io/change-cause="image updated to 1.10.1" -> add change cause
# kubectl rollout undo deployment deploy--recreate --to-revision 4   ----> rollback for  a specific version


step-6
scaling of apps:---
===================
# kubectl scale deployment deploy--recreate --replicas 10
deployment.apps/deploy-rolling scaled


============================================================
Strategy: BLUE GREEN DEPLOYMENT STRATEGY
============================================================
Blue-Green Deployment is a zero-downtime deployment strategy where you run two environments:

Blue = Current/Live/Production environment
Green = New version environment
Only one of them receives live traffic at a time.



DEMO: 15  blue green deployment 


step-1
     blue/old apps create:--
     -------------------------------
apiVersion: apps/v1                               
kind: Deployment                                  
metadata:                                         
 name: bluedeploy-originalprice                               
spec:                                             
 replicas: 6                                      
 selector:                                        
  matchLabels:                                    
       price: original                                      
 template:                                        
  metadata:                                       
   labels:                                        
       price: original                                     
  spec:                                           
   containers:                                    
   - name: test                                   
     image: quay.io/shruti1988/production:v1
     imagePullPolicy: IfNotPresent


 k apply -f <filename>.yaml
k get deployment
k get deployments.apps
k get deployment -o wide
k get pods -o wide

step-2
     create service :---
     ============
     # kubectl  expose deployment  bluedeploy-originalprice   --port 80 --target-port 80 --name blue-green-svc --type LoadBalancer
     
step-3
======
create green/new apps :--
====================
apiVersion: apps/v1                               
kind: Deployment                                  
metadata:                                         
 name: greendeploy-saleprice                              
spec:                                             
 replicas: 7                                      
 selector:                                        
  matchLabels:                                    
     price: sale                                    
 template:                                        
  metadata:                                       
   labels:                                        
      price: sale                                   
  spec:                                           
   containers:                                    
   - name: exam                                   
     image: quay.io/shruti1988/production:v1
     imagePullPolicy: IfNotPresent 

 k apply -f <filename>.yaml
k get deployment
k get deployments.apps
k get deployment -o wide
k get pods -o wide
     

step-4
     switch your service to the new/green deployment:--
         # kubectl edit svc blue-green-svc
 change the selector 
   
   
 Canary deployment 
===============
step-1 create old apps:---
================
apiVersion: apps/v1
kind: Deployment
metadata:       
 name: old-deploy
spec:           
 replicas: 6    
 selector:      
  matchLabels:  
   app: common  
 template:      
  metadata:     
   labels:      
    app: common
  spec:         
   containers:  
   - name: test 
     image: quay.io/shruti1988/production:v1
     imagePullPolicy: IfNotPresent
 
 
 k apply -f <filename>.yaml
k get deployment
k get deployments.apps
k get deployment -o wide
k get pods -o wide                                   


step-2
create svc
# kubectl  expose deployment old-deploy --port 80 --target-port 80 --name combo-svc --type LoadBalancer


step-3
======
create new apps with same version with same selector:--
apiVersion: apps/v1                               
kind: Deployment                                  
metadata:                                         
 name: new-deploy                                 
spec:                                             
 replicas: 4                                      
 selector:                                        
  matchLabels:                                    
   app: common                                    
 template:                                        
  metadata:                                       
   labels:                                        
    app: common                                   
  spec:                                           
   containers:                                    
   - name: exam                                   
     image: quay.io/shruti1988/production:v1
     imagePullPolicy: IfNotPresent 
     
     
    
 k apply -f <filename>.yaml
k get deployment
k get deployments.apps
k get deployment -o wide
k get pods -o wide  

===================================================================================================================
EXTRA KNOWLEDGE 

 A/B Testing Deployment
Different versions for different user groups.
 Shadow Deployment
New version gets copy of the traffic (mirrored), but users don’t see responses.    

===================================================================================================================

Environment variables 


Environment Variable:---

                           -------> we can add variables & values in our apps.
                           -------->  types
                           a> PlainKey
                           b> ConfigMap
                           c> Secret




mysql:---
MYSQL_USER--------  to create a new user account
MYSQL_PASSWORD    ------- to set password for the new user account
MYSQL_ROOT_PASSWORD   ------> to set user root password
MYSQL_DATABASE   --------> to craete a new database

DEMO22:  PlainKey 
vim plainkey.yaml

apiVersion: v1     
kind: Pod          
metadata:          
 name: plain-pod   
spec:              
 containers:       
 - name: xyz       
   image: quay.io/anshuk6469/mysql
   imagePullPolicy: IfNotPresent
   env:            
   - name: MYSQL_USER 
     value: tony   
   - name: MYSQL_PASSWORD
     value: redhat@123
   - name: MYSQL_ROOT_PASSWORD
     value: redhat1
   - name: MYSQL_DATABASE
     value: cka-shruti   


k apply -f plainkey.yaml
k get ppods -o wide               

how to test the variables & values:---
===========================
# kubectl describe pod plain-pod |less
            or
# kubectl  exec -it plain-pod /bin/bash
#env
# mysql -u tony -p
 show databases;

DEMO23: CONFIG-MAP

 ConfigMap/ cm:---
===========
step-1
create cm:---
   # kubectl  get cm  
   # kubectl  get cm 
   # kubectl  create cm myconfig --from-literal MYSQL_USER=shruti   --from-literal MYSQL_PASSWORD=redhat  --from-literal MYSQL_ROOT_PASSWORD=redhat --from-literal MYSQL_DATABASE=mydata

step-2
implement this cm in pod
--------------
apiVersion: v1    
kind: Pod        
metadata:         
 name: config-pod 
spec:             
 containers:      
 - name: xyz      
   image: mysql
   imagePullPolicy: IfNotPresent
   envFrom:       
   - configMapRef:  
      name: myconfig
      
DEMO24: SECRET 


step-1
create secret:---
==========
# kubectl  get secrets 
# kubectl  create secret generic  mysecret --from-literal MYSQL_USER=tony --from-literal MYSQL_PASSWORD=redhat@123 --from-literal MYSQL_ROOT_PASSWORD=redhat1 --from-literal MYSQL_DATABASE=baseball
# kubectl  describe secrets -n india mysecret 

step-2
implement secret in new pods/apps
======================
apiVersion: v1       
kind: Pod            
metadata:            
 name: secret-pod    
spec:                
 containers:         
 - name: xyz         
   image: mysql
   imagePullPolicy: IfNotPresent
   envFrom:          
   - secretRef:      
      name: mysecret


 for configmap as a volume:---

=====================
step1:

 kubectl  create cm myconfig --from-literal MYSQL_USER=shruti   --from-literal MYSQL_PASSWORD=redhat  --from-literal MYSQL_ROOT_PASSWORD=redhat --from-literal MYSQL_DATABASE=mydata

step-2
=====
create pod with configmap (as a volume)

apiVersion: v1                         
kind: Pod                              
metadata:                              
 name: cka-training-pod                
                
spec:                                  
 containers:                           
 - name: xyz                           
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent       
   volumeMounts:                       
   - name: koenig                     
     mountPath: /usr/share/nginx/html/
 volumes:                              
 - name: koenig                        
   configMap:                          
    name: myconfig                 
                 

step-3
access the pod & check:--

# kubectl  exec -it cka-training-pod /bin/sh
# cd /usr/share/nginx/html/






check where the pod got created
suppose it got created on node1 
then 
 go to node1 and type
 find / -name koenig 


Annotation


An annotation is a way to attach extra information (metadata) to objects like Pods, Services, Deployments, etc.
Annotation = key-value pair used to store additional details
👉 It is mainly for humans or tools, not for Kubernetes scheduling decisions

apiVersion: v1
kind: Pod
metadata:
  name: anno-pod
  annotations:
    description: " this is a pod for dev-app java"
    onwer: " this belong to dev team "
spec:
  containers:
  - name: cont1
    image: nginx
--------------------------------------------------------------------------------------------------
 Security Context 
 
Reference DOC: https://man7.org/linux/man-pages/man7/capabilities.7.html
 
apiVersion: v1             
kind: Pod                  
metadata:                  
  name: test-pod1          
  labels:                  
    color: blue            
spec:                      
  containers:              
  - name: cont1            
    image: quay.io/shruti1988/webapp
    securityContext:       
      capabilities:        
        add: [ "NET_RAW" ]

 --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 DAY5:
     MCQ or qubits :   https://www.qubits42.com/live/57437
     create a cluster on azure under ur name..
     
  Topics to cover today :
      1. Storage 
      2. stateless and stateful 
      3.security (RBAC)  and services account 
      4. cronjob 
      5.  logging and monitoring  ( time permits) 
      ---------------------------------------------------------------------------------------------------------
      
         
 Storage
Static Storage 
Admin creates storage manually in advance
Creates PersistentVolume (PV) first
User creates PersistentVolumeClaim (PVC)
PVC binds to an existing PV

Flow
Storage → PV (Admin) → PVC (User) → Pod

Characteristics

✔ Manual process
✔ Fixed size
✔ Less flexible
❌ Storage may be wasted
❌ Not scalable

Example Use Case
On-prem clusters
Legacy storage systems
When admin wants full control


Dynamic Volume Provisioning

Storage is created automatically
No need to create PV manually
Kubernetes provisions storage on demand

Flow
PVC → StorageClass → Storage → PV → Pod

Characteristics
✔ Automatic
✔ Scalable
✔ Cloud-friendly
✔ Preferred in production

Example Use Case
AWS EBS
Azure Disk
GCP Persistent Disk
CSI drivers


EPHERMAL STORAGE 

 ephemeral/temp storage:---
 concept  -----> emptyDir
 pod creates --------> /var/lib/kubelet/pods
 
 vime filename.yaml
 
 apiVersion: v1  
kind: Pod       
metadata:       
 name: testpod  
 namespace: india       
spec:           
 containers:    
 - name: xyz    
   image: quay.io/gauravkumar9130/mywebapp
   imagePullPolicy: IfNotPresent
   volumeMounts:        
   - name: school       
     mountPath: /student
 volumes:       
 - name: school 
   emptyDir: {}

k get pods -o wide 
kubectl exec -it testpod /bin/bash
cd /
ls -l
mkdir family
touch brother

go to worker1
find / -name family
cd / var/lib/kubelet/pods/8353nffrj0/ed


CREATING PERSISTENCE STORAGE 
PV ---- PVC ---POD 


 Creating persistence storage 
vim pv.yaml


apiVersion: v1  
kind: PersistentVolume            
metadata:     
 name: pv1    
spec:         
 accessModes: 
 - ReadWriteMany
 storageClassName: csi-hostpath-sc
 capacity:    
  storage: "5Gi"
 hostPath:    
  path: /shruti-vol

# kubectl  get pv


step-2 creating the pvc
vim pvc.yaml

apiVersion: v1                    
kind: PersistentVolumeClaim       
metadata:         
 name: pvc1       
          
spec:             
 accessModes:                     
 - ReadWriteMany                  
 storageClassName: csi-hostpath-sc
 resources:       
  requests:       
   storage: "5Gi"

k apply -f pvc.yaml                  
# kubectl  get pvc -n app

step-3 giving the pvc to pod 
vim pv-pvc-pod.yaml

create pods:---
==========
apiVersion: v1           
kind: Pod                
metadata:                
    
 namespace: app     
spec:                    
 containers:             
 - name: xyz             
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent
   volumeMounts:         
   - name: king          
     mountPath: /unique    
 volumes:                
 - name: king            
   persistentVolumeClaim:
    claimName: pvc1
    



k apply -f pv-pvc-pod.yaml
k exec -it pv-pvc-pod  -n app
cd /unique
mkdir subject ; cd subject
cat > english
hello i m learning english and k8s
ctrl+d

now check on which worker node the pod is allocated 
root@worker1:   cd /lion


storageClass defines how storage is dynamically provisioned in Kubernetes.

👉 Think of it as a storage template that tells Kubernetes:
What type of storage to create
From where
With which rules

Without StorageClass → manual (static) provisioning
With StorageClass → automatic (dynamic) provisioning

 Dynamic provisiong 
 
 Persistent Volume (Dynamic)
# kubectl get sc

# vim pvc.yml

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-pvc
spec:
  resources:
    requests:
      storage: 5G
  accessModes:
    - ReadWriteOnce
  storageClassName: managed-csi
  
# kubectl apply  -f pvc.yml


---------------
vim webapp.yml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      volumes:
      - name: myvol
        persistentVolumeClaim:
          claimName: dynamic-pvc
      containers:
      - name: webapp
        image: nginx
        volumeMounts:
        - name: myvol
          mountPath: /data-newly 

# kubectl create -f webapp.yml
# kubectl get pvc
# kubectl get pv

----------    
vim sc.yml


apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: shruti-disk
provisioner: disk.csi.azure.com
reclaimPolicy: Retain
volumeBindingMode: Immediate 
allowVolumeExpansion: true
parameters:
  skuName: StandardSSD_LRS
  location: centralus

 k apply -f sc.yml
 
-------------------------------------------------------------------
STATEFUL

vim sc.yaml


apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: local
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer


vim pv11. yaml


 apiVersion: v1
 kind: PersistentVolume
 metadata:
   name: pv11
 spec:
   accessModes:
   - ReadWriteMany
   storageClassName: local
   capacity:
     storage: "1Gi"
   hostPath:
     path: /mnt/data


apiVersion: apps/v1
kind: StatefulSet
metadata:
 name: mystate
spec:
 volumeClaimTemplates:
 - metadata:
    name: mystate-pvc
   spec:
    accessModes:
    - ReadWriteMany
    storageClassName: local
    resources:
     requests:
      storage: 500M
 replicas: 3
 template
  metadata:
   labels:
    app: db
  spec:
   containers:
   - name: c1
     image: quay.io/anshuk6469/mysql 
     imagePullPolicy: IfNotPresent
     env:
     - name: MYSQL_ROOT_PASSWORD
       value: root123
     volumeMounts:
     - name: mystate-pvc
       mountPath: /mnt
       
 selector:
  matchLabels:
   app: db


0/3 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/3 nodes are available: 3 Preemption is not helpful for scheduling.
-0 
-1
-2


Module 10 – Security 
Role BAsed Access Control)
           -------> we can assign  privelege to user & sa 
           --------> area types
           a> namespace wide:---
                        ------> it will be applicable for that ns only
                        -------> role & rolebinding
                        --------> role= verb/task(create/delete/get/list) + resource (pods/deployments/services.....)
                        ---------> rolebinding -----> to assign the role to the sa or user a/c for the ns

  ON RBAC 
git clone https://github.com/gauravkumar9130/kube-user
# cd kube-user/
# chmod +x user_script.sh 
# ./user_script.sh



# kubectl  get role 
# kubectl  get role -n dubai
# kubectl create role -n dubai my-role1 --verb=create,delete,list,get --resource=pods,deployments,services 
# kubectl  describe role -n dubai my-role1 

now rolebindinig:---
=============
# kubectl  get rolebindings.rbac.authorization.k8s.io -n india 1
# kubectl  create rolebinding -n dubai my-bind1 --role my-role1 --user shruti
# kubectl  create rolebinding -n dubai my-bind2 --role my-role1 --serviceaccount -n india
# kubectl delete rolebindings.rbac.authorization.k8s.io -n india my-bind1


kubectl auth can-i create pod --as shruti -n dubai 
  926  kubectl auth can-i delet pod --as shruti -n dubai 
  927  kubectl auth can-i delete pod --as shruti -n dubai 
  928  kubectl auth can-i get pod --as shruti -n dubai 
  929  kubectl auth can-i get sts --as shruti -n dubai 
  930  kubectl auth can-i get rc --as shruti -n dubai 
  931  kubectl auth can-i get svc --as shruti -n dubai
  
  
THROUGH DECLERATIVE WAY 
Create Role
https://kubernetes.io/docs/reference/access-authn-authz/rbac/

DEMO31:   RBAC WITH DECLATIVEWAY 

# vim role.yml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
 name: ckad-user-rol
rules:
 - resources: ["pods", "deployment"]
   verbs: ["get", "watch",]
   apiGroups: [""]
   
 # kubectl create -f role.yml
 k get role 
 
 # vim role-bind.yml 
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
 name: ckad-bind
subjects:
- kind: User
  name: ckad
  apiGroup: rbac.authorization.k8s.io
roleRef:
 kind: Role
 name: ckad-user-role
 apiGroup: rbac.authorization.k8s.io

  
 # kubectl create -f role-bind.yml
-------------------------------------------------------------------------------------------------------------------


Cluster Roles and Role Binding
kubectl create clusterrolebinding cluster-bind1  --clusterrole=admin --user=shruti
kubectl get clusterrolebinding 
k describe clusterrolebinding cluser-bind1
kubectl create clusterrole  shruti-cluster --verb=get,list, --resource=pods,deployments
kubectl get clusterrole
kubectl describe clusterrole shruti-cluster 




# vim cluster.yml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
 name: cluster-ckad
rules:
- apiGroups: [""]
  resources: ["nodes", "namespaces", "secrets",]
  verbs: ["get", "watch", "list"]

# kubectl create -f cluster.yml

# vim cluster-bind.yml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
 name: ckad-cluster
subjects:
- kind: User
  name: ckad
  apiGroup: rbac.authorization.k8s.io
roleRef:
 kind: ClusterRole
 name: cluster-ckad
 apiGroup: rbac.authorization.k8s.io

# kubectl create -f cluster-bind.yml



======================================================================================================================


SERVICE ACCOUNT 



how to create a new sa:---
=============
apiVersion: v1    
kind: ServiceAccount
metadata:         
 name: sa-demo

       or
 # kubectl  create sa new-sa 

how to attach a new pod with a new sa:---
===============================
apiVersion: v1                
kind: Pod                     
metadata: 
  name: sa-pod                               
spec:                         
 containers:                  
 - name: xyz                  
   image: quay.io/shruti1988/webapp
   imagePullPolicy: IfNotPresent
 serviceAccountName: sa-demo


==============================================================================================================
CRON JOB 


# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday)
# │ │ │ │ │                                   OR sun, mon, tue, wed, thu, fri, sat
# │ │ │ │ │
# │ │ │ │ │
# * * * * *



apiVersion: batch/v1
kind: CronJob
metadata:
  name: hello
spec:
  schedule: "* * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: hello
            image: busybox:1.28
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure



kubectl delete cronjob hello


uses case can be 
- backup
- log cleanup or logrotate
- sending email at specific time 
- securtity scan 


-------------------------------------------------
Application resource requirement 

- resource quota 

ResourceQuota in Namespace:---
========================

for compute resource:--
==================
requests: ----> minimum
       requests.memory: 300Mi
       
limits----> maximum
   limits.memory: 700Mi
   
# kubectl  get resourcequotas 
# kubectl  get resourcequotas  -n india 

apiVersion: v1
kind: ResourceQuota
metadata: 
 name: govt-quata
 namespace: india
spec:
 hard:
  pods: "10"
  services: "3"
  requests.memory: "500Mi"
  requests.cpu: "200m"  
  limits.memory: "800Mi"
  limits.cpu: "450m"

# kubectl  get resourcequotas -n india 
How to creata a ressource inside a ns with resource quota:---
===============================================       
apiVersion: v1       
kind: Pod       
metadata:       
  name: thurssday    
  namespace: india   
spec:           
  containers:   
  - name: cont1      
    image: quay.io/gauravkumar9130/mywebapp
    resources:       
     requests:       
      memory: "100Mi"
      cpu: "10m"     
     limits:    
      memory: "250Mi"
      cpu: "15m"

    
    
    How to change resourceQuota of a a ns:----
    
    # kubectl  edit resourcequotas -n india govt-quata 
    change the values that is required
    
    How to get manifests file in k8s:---
    # kubectl get deployment -n india training -o yaml > kolkata.yml

How to set the default ns:---
====================
# kubectl  config set-context  clustername 
# kubectl  config get-contexts 
 kubectl  config use-contexts
=========================================


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

feedback : https://rms.koenig-solutions.com/InterimFeedback.aspx?id=b2b6bab5b5bd&frm=3

DAY6:
    1. Liveness and Readiness
    2. Helm chart
    3. logging and monitoring
    4. auto-scaling 
   5.  AP-Deperication
    6. CRD
    7.networking  policy 
    8. Ingress nginx with small project 
 
    
mcq:  https://www.qubits42.com/live/57470
        check the testing tool with client selenium or junit
   Liveness probe:---  (for ckad only)
===============
JUst imagine that your apps has hang for long time--- but k8s will thinks that everything is fine and it will send customer traffic to the apps.
But if we use liveness probe ------ k8s detects that the app is no longer serving requests & kubelet will restart the problemectric pod and apps will run again.




Labs:---
======

apiVersion: v1
kind: Pod
metadata:
 name: liveness-exec
 labels:
  test: liveness
spec:
 containers:
 - name: liveness
   image: quay.io/gauravkumar9130/jenkins
   imagePullPolicy: IfNotPresent
   livenessProbe:
    exec:
     command: ["ls","/usr/share/jenkins/jenkins.war"]
    initialDelaySeconds: 5
    periodSeconds: 5


 k get pods 
 k  describe pod liveness-exec


 k  exec -it liveness-exec -- bash 
 cat  /usr/share/jenkins/jenkins.war
 java -jar jenkins.war
 
 Readiness of Pods:---  
================

These are of three types:---
a> command
b> http
c> tcp

command:--  for command probes, k8s runs a command inside your container. if the command returns with exit code 0--- container is healthy. Otherwise, it is marked unhealthy.

readinessProbe:
  exec:
   command: ["cat"."/tmp/health"]      # 0 is healthy 
  initialDelaySeconds: 5
  periodSeconds: 6



http:--
Establish an http request to the pod, k8s pings a path. and if it gets an HTTP response in the 200 or 300 range, it marks the app as healthy.... otherwise it will marks the apps as unhealthy.

readinessProbe:
  httpGet:
   path: /login
   port: 8080
  initialDelaySeconds: 5
  periodSeconds: 6

          
           TCP:-- It is the last type of probe, where k8s tries to establish a tcp connection on the specified port. if it can establish a connection... the container is considered healthy.
           
           
readinessProbe:
  tcpSocket:
   port: 80
  initialDelaySeconds: 5
  periodSeconds: 6





LAB for readiness:---

Step-1 (configure service)

apiVersion: v1     
kind: Service      
metadata:          
 name: abc         
spec:              
 type: LoadBalancer
 selector:         
  test: readiness  
 ports:            
 - targetPort: 8080
   port: 8080 




step-2 (configure Readiness with http probe for readiness)
=========
apiVersion: apps/v1    
kind: Deployment       
metadata:              
 name: readiness-exec  
 labels:               
  test: readiness      
spec:                  
 replicas: 5           
 selector:             
  matchLabels:         
   test: readiness     
 template:             
  metadata:            
   labels:             
    test: readiness    
  spec:                
   containers:         
   - name: app-ready       
     image: quay.io/gauravkumar9130/jenkins
     imagePullPolicy: IfNotPresent
     readinessProbe:           #         -------->  additional entry for Readiness    (http probe)
      httpGet:         
       path: /login    
       port: 8080      
      initialDelaySeconds: 5
      periodSeconds: 5             #   -----------> upto this 

k get svc -o wide 
copy ip of external loadbalancer nd paste iit in the brosswer 172.25.230.13:8080

k describe pod
k describe deployment  


==========================================================================================
HELM 


https://artifacthub.io/


Helm
=========
Helm Installation
==================
#curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
#chmod 700 get_helm.sh
#./get_helm.sh

Repositories Websites:
1) https://artifacthub.io

Work with Bitnami Repository
=============================
#helm repo add bitnami https://charts.bitnami.com/bitnami
#helm repo list 
#helm repo update
#helm search repo bitnami
#helm search repo bitnami | grep nginx
#helm install webserver bitnami/nginx
#helm list 
#kubectl get pods,svc
#helm uninstall webserver

Helm Commands:
To add helm repository:
        #helm repo add <repository name> <repository url>

To remove helm repository:
        #helm repo remove <repository name>

To search helm charts from repository:
        #helm search repo <repository name>
        
To list added repositories:
        #helm repo list 
        
To remove repositories:
        #helm repo remove <repository name>
        
To list installed helm charts:
        #helm list 
        
To install helm chart:
        #helm install <revisionname> <repositoryname>/<chartname> 

To install helm chart in different namespace:
        #helm install <revisionname> <repositoryname>/<chartname>  -n dashboard --create-namespace 
        
To remove helm chart:
        #helm uninstall <revision name>





Prometheus & Grafana  --------
-------------------------------------
prometheus ------- log collection tool -----> 
 grafana -------> create a monitoring dashboard

 INTEGRATING PROMETHEUS AND GRAFANA 
$ git clone https://github.com/gauravkumar9130/grafana
$ kubectl create -f 1-prometheus/.
$ kubectl create -f 2-grafana/.
$ kubectl get ns   ------------------> one new ns will be created with the name of monitoring
$ kubectl get pods -n monitoring
$ kubectl get svc -n monitoring

default user---- admin
            password --- admin
            
            dashboard----> import--->https://grafana.com/grafana/dashboards/15661-k8s-dashboard-en-20250125/  ----> load ----> select prometheus ----> prometheus--->
            
            
            
Horizontal Pod Autoscaler 
# kubectl get hpa
# kubectl get hpa -A

# vim nginx.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-hpa
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-web
        image: quay.io/shruti1988/webapp
        resources:
          requests:
            cpu: "100m"
          limits:
            cpu: "500m"

# kubectl create -f nginx.yml
# kubectl get pod
# kubectl get deployment

# kubectl expose deployment nginx-hpa --port=80 --target-port=80 --type=LoadBalancer --name=webapp
# kubectl get svc  -> Copy External IP

# vim hpa.yml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-hpa
  minReplicas: 1
  maxReplicas: 30
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50

# kubectl create -f hpa.yml
# kubectl get hpa

If you have Linux machine you can send traffice to the app for simulation
# while true; do curl http://4.249.169.146 > /dev/null; done
# ab -n 50000 -c 500 http://<EXTERNAL-IP>/


# kubectl get hpa -w
======================
kubectl autoscale deployment my-app --cpu-percent=50 --min=1 --max=5



=================================================================================================================
DAY7 : (Wednesday)
    
MCQ:   https://www.qubits42.com/live/57486

Networking
Ingress-Nginx
API-DEPRICATION
Debugging
Sentinel policy 


Reference yaml to create three pods  with label named =blue,black and green 

apiVersion: v1             
kind: Pod                  
metadata:                  
  name: test-pod1          
  labels:                  
    color: blue            
spec:                      
  containers:              
  - name: cont1            
    image: quay.io/shruti1988/webapp
    securityContext:       
      capabilities:        
        add: [ "NET_RAW" ]



NETWORK POLICY: 
=============
--------> it is a firewall rule/ packet filtering tech  in k8s cluster
--------> we can implement network policy for incoming/ingress or outgoing/egress packets
             
             incoming packets-------> ingress
             outgoing packets -------> egress
             
    labs:---
    # kubectl  get networkpolicies.
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:         
 name: mypolicy   
spec:             
 podSelector:     
  matchLabels:    
   color: black     
 policyTypes:     
 - Ingress        
 - Egress         
 ingress:         
 - from:          
   - podSelector: 
      matchLabels:
       color: green 
                  
 egress:          
 - to:            
   - podSelector: 
      matchLabels:
        color: blue



K get  networkpolicy
k describe networkpolicy mypolicy

[root@master ~]#  k get pods -o wide --show-labels | grep -i test-pod
test-pod1                         1/1     Running            0                 5d18h   10.244.166.134   node1   <none>           <none>            color=blue
test-pod11                        1/1     Running            0                 25m     10.244.104.21    node2   <none>           <none>            color=black
test-pod12                        1/1     Running            0                 24m     10.244.104.24    node2   <none>           <none>            color=green
test-pod13                        1/1     Running            0                 24m     10.244.104.25    node2   <none>           <none>            color=blue

[root@master ~]# k exec -it test-pod11 -- sh 
/opt # ping -c3 10.244.104.24
PING 10.244.104.24 (10.244.104.24): 56 data bytes

--- 10.244.104.24 ping statistics ---
3 packets transmitted, 0 packets received, 100% packet loss
/opt # ping -c3 10.244.104.25
PING 10.244.104.25 (10.244.104.25): 56 data bytes
64 bytes from 10.244.104.25: seq=0 ttl=63 time=0.201 ms
64 bytes from 10.244.104.25: seq=1 ttl=63 time=0.092 ms
64 bytes from 10.244.104.25: seq=2 ttl=63 time=0.107 ms

--- 10.244.104.25 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.092/0.133/0.201 ms
/opt # exit 


INGRESS-CONTROLLER 
 INGRESS CONTROLLER - HOTEL APPLICATION DEPLOYMENT 
(for both cloud & on-prem k8s cluster)
==========================
step-1
install ingress:---
# git clone https://github.com/kubernetes/ingress-nginx
# cd ingress-nginx/deploy/static/provider/cloud/
# kubectl  apply -f deploy.yaml 
# kubectl get ns     -------> to see ingress-nginx ns created




step-2
create apps:---
==========
# kubectl  create deploy hotel --image quay.io/shruti1988/hotel --replicas 5
# kubectl  create deploy tea --image quay.io/shruti1988/tea --replicas 5
# kubectl  create deploy coffee --image quay.io/shruti1988/coffee --replicas 5


step-3
create LoadBalancer for individual apps:---
=====================
# kubectl  expose deployment hotel --port 80 --target-port 80 --name hotel-svc --type LoadBalancer
# kubectl  expose deployment tea --port 80 --target-port 80 --name tea-svc --type LoadBalancer
# kubectl  expose deployment coffee --port 80 --target-port 80 --name coffee-svc --type LoadBalancer

step-4
======
create ingress routing rule:---
=======================
# kubectl get ingress



apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
 name: hotel-ingress
spec:
 ingressClassName: nginx
spec:
 rules:
 - http:
    paths:
    - path: /hotel
      pathType: Prefix
      backend:
       service:
        name: hotel-svc
        port:
         number: 80
    - path: /tea
      pathType: Prefix
      backend:
       service:
        name: tea-svc
        port:
         number: 80
    - path: /coffee
      pathType: Prefix
      backend:
       service:
        name: coffee-svc
        port:
         number: 80

k apply -f filename.yaml
k get svc -n ingress-nginx 
copy ip addrss of load balancer and paste it

CNI (Container Network Interface)
It is a standard framework used by Kubernetes to set up networking for Pods.
👉 In simple words:
CNI is responsible for giving Pods IP addresses and enabling Pod-to-Pod communication.
Why CNI is Needed
Kubernetes requirements:
Every Pod must get a unique IP
Pods should communicate
Pod ↔ Pod
Pod ↔ Service
Pod ↔ External world
Kubernetes does not implement networking itself.
It uses CNI plugins to do this job.
     





Manage Networking
=====================

Custom DNS for Pod
------------------------
#vim pod.yml
apiVersion: v1
kind: Pod
metadata:
 name: abc
spec:
 hostAliases:
 - ip: "1.1.1.1"
   hostnames:
   - "shruti.com"
 - ip: "2.2.2.2"
   hostnames:
   - bruno.com
 containers:
 - name: abc
   image: nginx

=============================================================================
CRD (Custom Resource Definition) in Kubernetes


A CRD lets you extend Kubernetes by creating your own resource types, just like built-in ones such as Pods or Deployments.
CRD = way to define your own Kubernetes object

Discover and Use Resources that Extend Kubernetes (CRD)

Custom Resource Doc :
https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/

Custom Resource Definitaion Doc :
 https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/
 
Sample Controller:
https://github.com/kubernetes/sample-controller


apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: crontabs.web.apps
spec:
  group: web.apps
  versions:
  - name: v1
    served: true
    storage: true
    schema:
      openAPIV3Schema:
        type: object
        properties:
          cronSpec:
            type: string
          image:
            type: string
          replicas:
            type: integer
  scope: Namespaced
  names:
    plural: crontabs
    singular: crontab
    kind: CronTab
    shortNames:
    - ct


# kubectl create -f crd-sample.yml
# kubectl get crd

# vim cr-sample.yml
cr-sample.yml 
apiVersion: web.apps/v1
kind: CronTab
metadata:
  name: my-new-cron-object
spec:
  cronSpec: "* * * * */5"
  image: nginx
  
  # kubectl create -f cr-sample.yml
  # kubectl get crontab


SENTINEL POLICY 
https://www.sentinelone.com/cybersecurity-101/cloud-security/kubernetes-security-policy/

Debugging 
 
 
 
 depricated
 https://kubernetes.io/docs/reference/using-api/deprecation-guide/
 *****************************************************************************************************************************************
 END OF CKAD AND AKS
 *****************************************************************************************************************************************
 
