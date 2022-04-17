## goldboot

`goldboot` automates the process of building bare-metal golden images from scratch.

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

### Image Templates

`goldboot` comes with a variety of base templates that function as a starting point
for building new images. For example, the `Windows10` base template can be used to
get a clean Windows 10 instance which can then be subjected to custom provisioning.

### Multi Boot

Provisioning multiple operating systems on the same disk is supported by adding multiple
base templates to `goldboot.json`.

For example, it's possible to build a dual-boot Windows10 / ArchLinux image by simply:

```sh
goldboot init --template Windows10 --template ArchLinux
```

### Directories

#### Media Cache

The media cache stores install media that must be downloaded from the Internet.
Files here are named by the SHA1 hash of their URL.

| Platform | Location                          |
|----------|-----------------------------------|
| Linux    | `/var/lib/goldboot/media_cache`   |
| macOS    |
| Windows  |

#### Image Library

The image library contains final build artifacts. Files here are named by the SHA1
hash of their contents.

| Platform | Location                     |
|----------|------------------------------|
| Linux    | `/var/lib/goldboot/images`   |
| macOS    |
| Windows  |

### BIOS Support

### Build Process

#### Fetch install media

Download ISOs and verify checksums.

#### Allocate qcow2 image

#### Run partitioner

#### Launch QEMU VM

#### Connect VNC

#### Connect SSH

#### Run provisioners

#### Install bootloader

#### Compact final image