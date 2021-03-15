



## Install
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-latest.x86_64.rpm
rpm -ivh minikube-latest.x86_64.rpm
```

```
PATH=$PATH:/usr/bin
echo $PATH
```
#### docker 설치
```
yum install docker
systemctl enable docker
systemctl start docker
```

#### kubectl 설치
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```
```
yum install -y kubectl
```

#### minikube 시작
```
minikube start
```
X Exiting due to DRV_AS_ROOT: The "docker" driver should not be used with root privileges.

```
minikube start --driver=none
```
X Exiting due to GUEST_MISSING_CONNTRACK: Sorry, Kubernetes 1.20.2 requires conntrack to be installed in root's path

```
yum install conntrack
```

```
minikube start --driver=none
```
<details><summary>결과화면</summary>
* minikube v1.18.1 on Centos 7.3.1611 (kvm/amd64)  
* Using the none driver based on user configuration  
* Starting control plane node minikube in cluster minikube  
* Running on localhost (CPUs=4, Memory=3790MB, Disk=102388MB) ...  
* OS release is CentOS Linux 7 (Core)  
    > kubelet: 108.73 MiB / 108.73 MiB [-------------] 100.00% 7.17 MiB p/s 16s  
  - Generating certificates and keys ...  
  - Booting up control plane ...  
  - Configuring RBAC rules ...  
* Configuring local host environment ...  
*  
! The 'none' driver is designed for experts who need to integrate with an existing VM  
* Most users should use the newer 'docker' driver instead, which does not require root!  
* For more information, see: https://minikube.sigs.k8s.io/docs/reference/drivers/none/  
*  
! kubectl and minikube configuration will be stored in /root  
! To use kubectl or minikube commands as your own user, you may need to relocate them. For example, to overwrite your own settings, run:  
*  
  - sudo mv /root/.kube /root/.minikube $HOME  
  - sudo chown -R $USER $HOME/.kube $HOME/.minikube  
*  
* This can also be done automatically by setting the env var CHANGE_MINIKUBE_NONE_USER=true  
* Verifying Kubernetes components...  
  - Using image gcr.io/k8s-minikube/storage-provisioner:v4  
* Enabled addons: default-storageclass, storage-provisioner  
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default  
</details>




```
[root@localhost /]# kubectl get po -A
```
The connection to the server localhost:8080 was refused - did you specify the right host or port?







## Uninstall
```
minikube stop; minikube delete
docker stop (docker ps -aq)
rm -r ~/.kube ~/.minikube
sudo rm /usr/local/bin/localkube /usr/local/bin/minikube
systemctl stop '*kubelet*.mount'
sudo rm -rf /etc/kubernetes/
docker system prune -af --volumes
```

