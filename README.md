ansible_unregistervm_windows_newvmmounted
======================

This is an ansible role to perform unregister Windows VM before unmounting with Actifio.

This role covers removing Windows license key and unjoining computer from AD domain. 

Requirements
--------------

Ansible >= 2.5 and PyVmomi module are required.

Tested with Windows 2012R2 VM only but will be able to work with other Windows version if Powershell commands using tasks/main.yml are compatible with your Windows VM.


Role Variables
--------------

Following variables are accepted/required for this role. 

| Variable Name    | Description | Required (Y/N) |
|------------------|---|---|
| vc_server_ip     | vCenter server IP address. | Y               |
| vc_username      | vCenter username to issue shell command through vmware_vm_shell | Y
| vc_password      | Password for the vCenter user | Y
| vc_validate_certs    | Allows connection when SSL certificates are not valid. Set to false when certificates are not trusted. Default is false. | N
| tgt_datacenter   | Datacenter name where the VM belongs | Y
| tgt_vm_name      | Target VM name which will be customized with this role. | Y
| vmwin_adminuser      | Administrator user name of the target Windows VM. Default is 'Administrator' | Y
| vmwin_adminpassword  | Administrator user password of the target Windows VM. | Y
| vmwin_powershellpath | Powershell comand path of the target Windows VM. Default is 'C:\Windows\System32\WindowsPowershell\v1.0\powershell.exe'. | Y
| vmwin_ad_domain  | AD domain name of the target Windows VM. | N


Example Playbook
----------------

### Customize Windows VM after mounting image as New VM by Actifio

```
- name: customize windows vm after mounting image as new vm by actifio
  hosts: "{{ host_group }}"
  become: yes
  become_method: sudo
  roles:
    - { role: ansible_customizevm_windows_newvmmounted, vc_server_ip: 8.8.8.8, vc_username: administrator@vsphere.local, vc_password: password }
  vars:
    tgt_datacenter: Datacenter
    tgt_vm_name: DemoWin2012
    vmwin_adminpassword: password
    vmwin_ad_domain: demodomain

```


License
-------

Copyright 2018 <Hiroshi Takeuchi hiroshi.takeuchi@actifio.com>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
