## Steam Deck Dual-Boot

This guide will explain the necessary steps to build and deploy a dual-boot golden
image for the Steam Deck.

This process will necessarily erase all data on the device's SSD!

###### Initialize a new goldboot repository

```sh
mkdir MySteamDeck && cd MySteamDeck
goldboot init \
	--template SteamDeck \
	--template Windows10 \
	--memory 16G \
	--disk 512G
```

If your workstation has less than 16G memory, then it should be reduced in the
`init` command.

###### Fine tune the goldboot configuration

The config will looks something like the following:

```json
{
  "name": "MySteamDeck",
  "arch": "x86_64",
  "memory": "16G",
  "disk_size": "512G",
  "templates": [
    {
      "type": "SteamDeck",
      "disk_usage": "50%"
    },
    {
      "type": "Windows10",
      "disk_usage": "50%"
    }
  ],
}
```

By default, goldboot will split the total available storage size equally for both
installations. To adjust this, modify the `"disk_usage"` options (which should collectively
sum to 100% or less).

###### Build the image

This is the easy part. Start the build and wait (probably about 30 minutes):

```sh
goldboot build
```

###### Create bootable flash drive

Choose a USB drive to be erased:

```sh
sudo goldboot makeusb /dev/sdX --include MySteamDeck
```

###### Deploy the image

Boot the USB drive on the Steam Deck by holding volume down during power-on. Choose
the `MySteamDeck` image in the menu and the device's internal SSD as the destination.

Once the image is written to the SSD, remove the USB drive and you're done!