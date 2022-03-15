## goldboot

`goldboot` automates the process of building bare-metal golden images from scratch. Under
the hood, `goldboot` uses `packer` to provision QEMU virtual machines that match
the eventual hardware.

### Configuration

```py
{
	"name"        : String(), # The image name
	"description" : String(), # An optional image description
	"memory"      : String(), # The amount of memory to allocate to the VM
	"disk_size"   : String(), # The size of the disk to allocate to the VM
	"provisioners" : [
		{
			"type" : String(values=["shell", "ansible"]),
			"script_path" : String(),
			"playbook_path" : String(),
		}
	],
	"partitions" : [
		{
			"type": String(),
			"label": String(),
			"size": String(),
			"format": String(),
		}
	]
}
```

### Initialization

Before you can build your first golden image, you first need to initialize a directory. The
`goldboot init` command will examine your current hardware and produce a configuration
file `goldboot.json` (which should be checked into version control).

### Image Profiles

`goldboot` comes with a variety of base profiles that function as a starting point
for building new images. For example, the `Windows10` base profile can be used to
get a clean Windows 10 instance which can then be subjected to custom provisioning.

### Multi Boot

Provisioning multiple operating systems on the same disk is supported by adding multiple
base profiles to `goldboot.json`. It's not possible to provision more than one of the
same type of profile.

### BIOS Support

