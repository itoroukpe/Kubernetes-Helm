# Kubernetes-Helm
## Installing Helm
From The Helm Project
The Helm project provides two ways to fetch and install Helm. These are the official methods to get Helm releases. In addition to that, the Helm community provides methods to install Helm through different package managers. Installation through those methods can be found below the official methods.

## From the Binary Releases
Every release of Helm provides binary releases for a variety of OSes. These binary versions can be manually downloaded and installed.

Download your desired version
```
Installation and Upgrading
Download Helm v3.11.3. The common platform binaries are here:

MacOS amd64 (checksum / 9d029df37664b50e427442a600e4e065fa75fd74dac996c831ac68359654b2c4)
MacOS arm64 (checksum / 267e4d50b68e8854b9cc44517da9ab2f47dec39787fed9f7eba42080d61ac7f8)
Linux amd64 (checksum / ca2d5d40d4cdfb9a3a6205dd803b5bc8def00bd2f13e5526c127e9b667974a89)
Linux arm (checksum / 0816db0efd033c78c3cc1c37506967947b01965b9c0739fe13ec2b1eea08f601)
Linux arm64 (checksum / 9f58e707dcbe9a3b7885c4e24ef57edfb9794490d72705b33a93fa1f3572cce4)
Linux i386 (checksum / 09c111400d953eda371aaa6e5f0f65acc7af6c6b31a9f327414bb6f0756ea215)
Linux ppc64le (checksum / 9f0a8299152ec714cee7bdf61066ba83d34d614c63e97843d30815b55c942612)
Linux s390x (checksum / e8b0682166628a9c16bf185d60c3d766a8ff814bff362de88280ef202148fbec)
Windows amd64 (checksum / ae146d2a90600c6958bc801213daef467237cf475e26ab3f476dfb8e0d9549b7)
```
Unpack it (tar -zxvf helm-v3.0.0-linux-amd64.tar.gz)
Find the helm binary in the unpacked directory, and move it to its desired destination (mv linux-amd64/helm /usr/local/bin/helm)

## From Script
Helm now has an installer script that will automatically grab the latest version of Helm and install it locally.

You can fetch that script, and then execute it locally. It's well documented so that you can read through it and understand what it is doing before you run it.
```
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```
Yes, you can curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash if you want to live on the edge.

## From Apt (Debian/Ubuntu)
Members of the Helm community have contributed a Helm package for Apt. This package is generally up to date.
```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```
