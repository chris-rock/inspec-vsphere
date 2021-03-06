# InSpec VMware

This repository contains a collection of InSpec resources used to interact with the VMware platform.

> This resource pack requires an InSpec version greater than `2.2.34`

## Using this Resource Pack

In order to use the resources in this resource pack you must declare the dependency in your InSpec profile.

Example:

```yaml
depends:
  - name: inspec-vmware
    git: git@github.com:inspec/inspec-vmware.git
```

## Using the VMware Target

After defining a dependency on `inspec-vmware` in `your_profile` you are ready to use these resources with the `vmware://` target.

### Via Arguments

```shell
~$ inspec exec your_profile -t vmware://USERNAME@VISERVER --password MY_PASSWORD
```

### Via Environment Variables

```shell
~$ export VISERVER=10.0.0.10
~$ export VISERVER_USERNAME=demouser
~$ export VISERVER_PASSWORD=s0m3t1ngs3cuRe
~$ inspec exec inspec-vmware -t vmware://
```

### Via the InSpec Shell

```shell
~$ inspec shell -t vmware://USERNAME@VISERVER --password MY_PASSWORD --depends ./inspec-vmware
```

## Pre-Requisites

We have a [cookbook][cookbook] that can install PowerCLI leveraging Chef also.

### Windows

#### Install PowerCLI on Windows 2012R2

```powershell
PS > Invoke-WebRequest -Uri "https://download.microsoft.com/download/C/4/1/C41378D4-7F41-4BBE-9D0D-0E4F98585C61/PackageManagement_x64.msi" -OutFile PackageManagement.msi
PS > msiexec.exe /i C:\Users\vagrant\PackageManagement.msi /quiet
PS > Set-PSRepository -Name "PSGallery" -InstallationPolicy "Trusted"
PS > Install-Module -Name VMware.PowerCLI
```

#### Install PowerCLI on Windows 10, 2016+

```powershell
PS > Set-PSRepository -Name "PSGallery" -InstallationPolicy "Trusted"
PS > Install-Module -Name VMware.PowerCLI
```

### Linux

#### Install PowerCLI on Debian based OSs

```shell
~$ sudo apt-get install curl
~$ curl  https://packages.microsoft.com/keys/microsoft.asc > MS.key
~$ sudo apt-key add MS.key
~$ curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list
~$ sudo apt-get update
~$ sudo apt-get install -y powershell
~$ pwsh -Command "& {Set-PSRepository -Name PSGallery -InstallationPolicy Trusted}"
~$ pwsh -Command "& {Install-Module -Name VMware.PowerCLI -Force}"
```

#### Install PowerCLI on Redhat based OSs

```shell
~$ curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/microsoft.repo
~$ yum install powershell
~$ pwsh -Command "& {Set-PSRepository -Name PSGallery -InstallationPolicy Trusted}"
~$ pwsh -Command "& {Install-Module -Name VMware.PowerCLI -Force}"
```

## License

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

[cookbook]: https://supermarket.chef.io/cookbooks/powercli_install
