# vsphere-tf

vSphere with Terraform

Figuring out how to use Hashicorp suite to do VMWare things. Any borrowed code or references and learning material used will be linked below

---

## Usage

Install Prerequisites:

```sh
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install packer terraform whois
git clone https://github.com/ottter/vsphere-tf.git
```

Configure required sections:

```sh
mkpasswd -m sha-512 --rounds=4096
# Enter password in prompt and add output to vsphere-tf\packer-tek\http\user-data autoinstall => identity => password
```

```sh
cp packer-tek/variables.pkrvars-examples.hcl packer-tek/variables.pkrvars.hcl
```

- Edit `packer-tek/variables.pkrvars100GBdisk.hcl` and `packer-tek/variables.pkrvars.hcl` to fit template requirements

Run:

```sh
cd packer-tek
packer build -force -on-error=ask -var-file variables.pkrvars100GBdisk.hcl -var-file variables.pkrvars.hcl ubuntu-22.04.pkr.hcl
cd ../terraform
terraform init
terraform plan
terraform apply 
```

---

## Reference Material

### Docs

- [Install Packer](https://developer.hashicorp.com/packer/tutorials/docker-get-started/get-started-install-cli)
- [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- [HashiCorp: Manage VMs and Snapshots on vSphere](https://developer.hashicorp.com/terraform/tutorials/virtual-machine/vsphere-provider)
- [F5 VPN and Terraform](https://clouddocs.f5.com/products/orchestration/terraform/latest/userguide/configuring.html)

### Blogs

- [Terraform to Create a Ubuntu 22.04 VM in VMware vSphere ESXi](https://tekanaid.com/posts/terraform-create-ubuntu22-04-vm-vmware-vsphere)
- [HashiCorp Packer to Build a Ubuntu 20.04 Image Template in VMware](https://tekanaid.com/posts/hashicorp-packer-build-ubuntu20-04-vmware)
- [HashiCorp Packer to Build a Ubuntu 22.04 Image Template in VMware vSphere](https://tekanaid.com/posts/hashicorp-packer-build-ubuntu22-04-vmware)
- [Packer Build Ubuntu 22.04 for VMware vSphere](https://www.virtualizationhowto.com/2022/04/packer-build-ubuntu-22-04-for-vmware-vsphere/)

### Public repos

- [public-projects3/Terraform Ubuntu 22.04 VM in vSphere](https://gitlab.com/public-projects3/infrastructure-vmware-public/terraform-ubuntu-22.04-vm-in-vsphere/-/tree/main)
- [public-projects3/Vmware Packer Ubuntu22.04 Public](https://gitlab.com/public-projects3/infrastructure-vmware-public/vmware-packer-ubuntu22.04-public)
- [brandonleegit/PackerBuilds](https://github.com/brandonleegit/PackerBuilds)

### Videos

- [Terraform Creates a Ubuntu 22.04 VM in VMware vSphere](https://www.youtube.com/watch?v=hp8XcRNnBnU)
- [HashiCorp Packer to Build a Ubuntu 22.04 Image in VMware vSphere](https://www.youtube.com/watch?v=FvQuVWk2f6s)
