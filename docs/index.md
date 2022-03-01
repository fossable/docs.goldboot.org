##

`goldboot` automates the process of building golden images.

```py
{
	"name"        : String(), # The image name
	"description" : String(), # An optional image description
	"base"        : String(), # A base profile
	"user"        : {
		"username" : String(),
		"password" : String(),
	},
	"iso_url"      : String(),
	"iso_checksum" : String(),
	"provisioners" : [
		{
			"type" : String(values=["shell", "ansible"]),
			"script_path" : String(),
			"playbook_path" : String(),
		}
	]
}
```
