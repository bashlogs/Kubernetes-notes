# NFS Server

## Install NFS Server <a href="#install-nfs-server" id="install-nfs-server"></a>

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

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FOEnW8pjnlbUBXMCbimzE%252FScreenshot%2520from%25202024-01-21%252012-34-12.png%3Falt=media%26token=c6d5c848-1556-49f7-b3ce-a2df4bb8a076&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=e9cf820852b896afa6fd81d0eb10040ca6a4787d936347306e6ff1e6678f5b4d" alt=""><figcaption><p>Home Page</p></figcaption></figure>

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

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FwTHAx4lVCN5NchV4esVq%252FScreenshot%2520from%25202024-01-21%252012-34-20.png%3Falt=media%26token=612032be-9f42-4f39-9ab3-ffdb8605b73c&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=fd4bcaa6d0bd9c03350b7794e7c56a5960fdd5f59ba5b87b08917e86dea18b6b" alt=""><figcaption></figcaption></figure>

Step 4: Export the nfs directory

After granting access to the preferred client systems, export the NFS share directory and restart the NFS kernel server for the changes to come into effect.

```
sudo exportfs -arv
sudo systemctl restart nfs-kernel-server
```

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FtNftMV440BaeSKHF16bg%252FScreenshot%2520from%25202024-01-21%252012-36-57.png%3Falt=media%26token=8ca9f268-24d6-4936-90e1-842619c4851a&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ddbd3d0579810b6b0e9ed3fac3b53bc2b1072b91316253592b97c6ccb1a217fc" alt=""><figcaption></figcaption></figure>

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

#### **Step 2: Create an NFS Mount Point on Client** <a href="#step-2-create-an-nfs-mount-point-on-client" id="step-2-create-an-nfs-mount-point-on-client"></a>

```
sudo mkdir -p /mnt/nfs
```

#### **Step 3: Mount NFS Share on Client System** <a href="#step-3-mount-nfs-share-on-client-system" id="step-3-mount-nfs-share-on-client-system"></a>

To check if the server is exporting any directories, use the following command.

```
showmount --export <server_ip_addr>
```

Now mount the nfs directory to your directory

```
sudo mount <ip_add>:/mnt/nfs /mnt/nfs
```

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FlZYFQIN59PlQjDnk5Ol8%252Fimage.png%3Falt=media%26token=08f0c4ca-28ac-4fce-9545-a99aeac59b6c&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=701f6ecc9f5c05e74d448eb7cf5b36f9ab49946597a6d15bfccc3358097c852f" alt=""><figcaption></figcaption></figure>

#### Step 4: Check the connection. <a href="#step-4-check-the-connection" id="step-4-check-the-connection"></a>

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

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252Fx6rFmEt0TBvU3kYcIqOP%252Fimage.png%3Falt=media%26token=e8e1106b-1934-4f89-97eb-8b14d1a076ec&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=cc591eda29a301ce147c45750dbf349fc15b0d9ba9f810d6a39b1b47c6f47e0d" alt=""><figcaption></figcaption></figure>

## Installing Autofs <a href="#installing-autofs" id="installing-autofs"></a>

Autofs offers automounting functionality, automatically mounting the NFS directory when accessed.

#### Step 1: Un-mount the nfs directory <a href="#step-1-un-mount-the-nfs-directory" id="step-1-un-mount-the-nfs-directory"></a>

```
sudo umount /mnt/nfs
```

#### Step 2: Install autofs on your system <a href="#step-2-install-autofs-on-your-system" id="step-2-install-autofs-on-your-system"></a>

```
sudo apt install autofs // for debian system
sudo pacman -S autofs // For arch system
```

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FFaZLOzua5kTN2YN3QZjd%252Fimage.png%3Falt=media%26token=a3f85c1c-4900-4226-a996-3ade351af264&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6721e4b6904046b773854d92ccaa183eb00c3e7d1bfbd107a3795d08413dec18" alt=""><figcaption></figcaption></figure>

#### Step 3: Autofs Configurations <a href="#step-3-autofs-configurations" id="step-3-autofs-configurations"></a>

Edit the file '_/etc/autofs.master_' or '_/etc/autofs/autofs.master_' and add the following content.

```
/mnt/nfs /etc/autofs/autofs.nfs --ghost --timeout=60
```

Create the file '_/etc/autofs/autofs.nfs_' or '_/etc/autofs.nfs'_. Additionally, establish a 'backups' folder on the server side.

```
backups -fstype=nfs4,rw 192.168.0.106:/mnt/nfs
```

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FXEHQAn5qgD90k1ruxlFT%252Fimage.png%3Falt=media%26token=39881445-c349-4055-a677-1705f4d29fa1&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=f5bf0b15a03f78dedae5175daed5df4a250dd7578fc35502a263546cc1212f96" alt=""><figcaption></figcaption></figure>

Delete all mount points and restart the autofs service.

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FY2pbNxxuwxEbg78r5fXo%252Fimage.png%3Falt=media%26token=ea75817d-84de-48aa-9d6d-e7746dd49910&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=1866bbfdd489df2117d53699b8c04405f14738e531cfe87caa6ced57b2c1448e" alt=""><figcaption></figcaption></figure>

Check whether the NFS server is mounted or not.

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252FhBC8vmfDHv0IdWjJNYnD%252Fimage.png%3Falt=media%26token=e651a694-d428-4088-954e-a0f2a8a0af75&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=382f05f31e21f4a82622d0388ea34ff6fb4b6b3a0f0792f823e78cae3c20ae93" alt=""><figcaption></figcaption></figure>

The NFS server is currently not mounted. Now attempt to access the NFS directory.

<figure><img src="https://bashlogs.gitbook.io/~gitbook/image?url=https:%2F%2F2961128508-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FuAu6jYJqhZp7YpOWRmwI%252Fuploads%252Fgs0adiG3zpvX7MXZF4Vf%252Fimage.png%3Falt=media%26token=75fa7c5c-aef5-445c-bad0-78082736b8d3&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=95e8a0598778fb2e984cb647a4fe1566933d985b29cd0a63906c8e67ca2248b4" alt=""><figcaption></figcaption></figure>

The NFS server is now accessible, and it is mounted automatically when accessed.

## Source / Documentation

{% embed url="https://www.tecmint.com/install-nfs-server-on-ubuntu/" %}

{% embed url="https://medium.com/@osa_/how-to-set-up-an-nfs-server-and-client-in-an-ubuntu-environment-to-share-files-directories-388083f2fd3e" %}

{% embed url="https://youtu.be/Na_jKeVWzrc" %}
