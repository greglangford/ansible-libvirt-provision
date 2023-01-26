# ansible-libvirt-provision
This repository is a dirty example of using the virsh, cloud-localds and virt-install commands to provision virtual machines using generic cloud based images such as **debian-11-genericcloud-amd64.raw** the cloud-init configuration is created dynamically from templates the virtual machine is then provisioned using the cloud-init nocloud data source. Once the provision stage has completed the virtual machine will be made persistent and autostart without the nocloud image attached.

This is by no means a production ready example you should use it at your own risk. I created this out of necessity due to needing to provision a large number of virtual machines across a number of physical hosts. I make no gurantee that there will be any updates or bugfixes. If you like the code and want to improve it yourself please create a fork I would love to see what you do with it.

The encrypted passwords and public keys are to demonstrate the values required, they are not passwords or keys for anything real ... sorry :)

### Known issues
* task **"virt-install bootstrap stage"** will hang when the cloud-init data is invalid, because the command **__virt_install_bootstrap_stage_command_list** runs with --wait -1 the command will not exit until the virtual machine is shutdown. You could change this to --wait 300 to wait for 5 minutes max, bearing in mind if your cloud-init provisioning takes more than 5 minutes the command will fail anyway.