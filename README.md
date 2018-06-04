# kubernetes-nfs-storage
To do that we need a NFS server and a disk to storage volumes created by kubernetes.

## Install NFS
In server:
``` apt install nfs-common nfs-kernel-server -y ```
Clients:
``` apt install nfs-common ```

## Prepare disk to storage
Once nfs-server was installed, go to your partition or lvm and mount in directory:
``` mkdir -p /mnt/kube_nfs && mount /dev/mapper/k8s-lvm /mnt/kube_nfs ```

## Export disk
In /etc/exports put the next line:
``` /mnt/kube_nfs *(rw,sync,no_subtree_check) ```
And export:
``` exportfs -a ```

## Create yaml's in K8s:
``` kubectl create -f privs/ ```

Before create deployment.yaml you need change server IP and another values if you have personalize them.

``` kubectl create -f deploy/ ```

When all have already finish only just remain do a test:

``` kubectl create -f test-pvc.yaml ```
