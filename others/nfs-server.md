# NFS Server

Install NFS Server

### Step 1: Install nfs-kernel on the ubuntu <a href="#step-1-install-nfs-kernel-on-the-ubuntu" id="step-1-install-nfs-kernel-on-the-ubuntu"></a>

```
sudo apt update
```

```
sudo apt install nfs-kernel-server
```

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

### Step 2: Create an nfs repository <a href="#step-2-create-an-nfs-repository" id="step-2-create-an-nfs-repository"></a>

Create a nfs folder

```
mkdir /mnt/nfs
```

To enable access for all client machines to the shared directory, eliminate any constraints within the directory permissions.

```
sudo chown -R nobody:nogroup /mnt/nfs
```

You can also tweak the file permissions to your preference. Here’s we have given the read, write and execute privileges to all the contents inside the directory.

```
sudo chmod 777 /mnt/nfs/
```

<figure><img src="../.gitbook/assets/2.png" alt=""><figcaption></figcaption></figure>

### Step 3: Grant nfs directory access to clients <a href="#step-3-grant-nfs-directory-access-to-clients" id="step-3-grant-nfs-directory-access-to-clients"></a>

To allow access for all client machines to the shared directory, remove any existing restrictions in the directory permissions.

```
sudo mv /etc/exports /etc/exports.orig
```

Create a new file

```
sudo vi /etc/exports
```

Add the following content in /etc/exports file

```
/mnt/nfs  192.168.0.0/24(rw,sync,no_subtree_check)
```

<figure><img src="../.gitbook/assets/3.png" alt=""><figcaption></figcaption></figure>

### Step 4: Export the nfs directory <a href="#step-4-export-the-nfs-directory" id="step-4-export-the-nfs-directory"></a>

After granting access to the preferred client systems, export the NFS share directory and restart the NFS kernel server for the changes to come into effect.

```
sudo exportfs -arv
sudo systemctl restart nfs-kernel-server
```

<figure><img src="../.gitbook/assets/4.png" alt=""><figcaption></figcaption></figure>

## Install the NFS Client on the Client Systems <a href="#install-the-nfs-client-on-the-client-systems" id="install-the-nfs-client-on-the-client-systems"></a>

### Step 1: Install basic packages <a href="#step-1-install-basic-packages" id="step-1-install-basic-packages"></a>

Update the system

```
sudo apt update
```

Install nfs-common packages

```
sudo apt install nfs-common
```

### **Step 2: Create an NFS Mount Point on Client** <a href="#step-2-create-an-nfs-mount-point-on-client" id="step-2-create-an-nfs-mount-point-on-client"></a>

```
sudo mkdir -p /mnt/nfs
```

### **Step 3: Mount NFS Share on Client System** <a href="#step-3-mount-nfs-share-on-client-system" id="step-3-mount-nfs-share-on-client-system"></a>

To check if the server is exporting any directories, use the following command.

```
showmount --export <server_ip_addr>
```

Now mount the nfs directory to your directory

```
sudo mount <ip_add>:/mnt/nfs /mnt/nfs
```

<figure><img src="../.gitbook/assets/5.png" alt=""><figcaption></figcaption></figure>

### Step 4: Check the connection. <a href="#step-4-check-the-connection" id="step-4-check-the-connection"></a>

Add some files on server side.

```
cd /mnt/nfs
```

```
vim test1.txt
```

Now, verify the presence of the files on the client side.

```
ls -l /mnt/nfs
```

<figure><img src="../.gitbook/assets/6.png" alt=""><figcaption></figcaption></figure>

## Installing Autofs <a href="#installing-autofs" id="installing-autofs"></a>

Autofs offers automounting functionality, automatically mounting the NFS directory when accessed.

### Step 1: Un-mount the nfs directory <a href="#step-1-un-mount-the-nfs-directory" id="step-1-un-mount-the-nfs-directory"></a>

```
sudo umount /mnt/nfs
```

### Step 2: Install autofs on your system <a href="#step-2-install-autofs-on-your-system" id="step-2-install-autofs-on-your-system"></a>

```
sudo apt install autofs // for debian system
sudo pacman -S autofs // For arch system
```

<figure><img src="../.gitbook/assets/7.png" alt=""><figcaption></figcaption></figure>

### Step 3: Autofs Configurations <a href="#step-3-autofs-configurations" id="step-3-autofs-configurations"></a>

Edit the file '_/etc/autofs.master_' or '_/etc/autofs/autofs.master_' and add the following content.

```
/mnt/nfs /etc/autofs/autofs.nfs --ghost --timeout=60
```

Create the file '_/etc/autofs/autofs.nfs_' or '_/etc/autofs.nfs'_. Additionally, establish a 'backups' folder on the server side.

```
backups -fstype=nfs4,rw 192.168.0.106:/mnt/nfs
```

<figure><img src="../.gitbook/assets/8.png" alt=""><figcaption></figcaption></figure>

Delete all mount points and restart the autofs service.

<figure><img src="../.gitbook/assets/9.png" alt=""><figcaption></figcaption></figure>

Check whether the NFS server is mounted or not.

<figure><img src="../.gitbook/assets/9.avif" alt=""><figcaption></figcaption></figure>

The NFS server is currently not mounted. Now attempt to access the NFS directory.

<figure><img src="../.gitbook/assets/10.png" alt=""><figcaption></figcaption></figure>

The NFS server is now accessible, and it is mounted automatically when accessed.

## Source / Documentation

{% embed url="https://www.tecmint.com/install-nfs-server-on-ubuntu/" %}

{% embed url="https://medium.com/@osa_/how-to-set-up-an-nfs-server-and-client-in-an-ubuntu-environment-to-share-files-directories-388083f2fd3e" %}

{% embed url="https://youtu.be/Na_jKeVWzrc" %}
