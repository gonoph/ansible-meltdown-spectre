# ansible-meltdown-spectre
Ansible Playbook to run the Red Hat spectre-meltdown check script for CVE-2017-5754 CVE-2017-5753 CVE-2017-5715.

Aka: Spectre and Meltdown Kernel side-channel attacks.

# Usage
1. Set your inventory under [Check]
2. Ensure `ansible_user` variable is **root**
3. Make sure `ScriptUrl` variable is set appropriately.
4. Make sure `ScriptGpgSigUrl` variable is set correctly - if you want to verify the GPG2 signature of the script.

You can run the playbook like so:

```bash
ansible-playbook -i inventory site.yml
```

Playbook will automatically download the check script and verify the GPG2 signature if the `ScriptGpgSigUrl` variable is defined.

Hosts that are vulnerable will show up as **failed** with a message of what vulnerabiliy was found. Additionally under the `highlight vulnerabilites` task, you will see the vulnerability that was found as a **changed** task.

```
TASK [highlight vulnerabilites] ******
ok: [store1] => (item=Spectre1)
ok: [oldgw] => (item=Spectre1)
changed: [oldgw] => (item=Spectre2)
ok: [oldgw] => (item=Meltdown)
changed: [store1] => (item=Spectre2)
ok: [store1] => (item=Meltdown)

TASK [Error if vulnerabilities] ******
fatal: [store1]: FAILED! => {"changed": false, "failed": true, "msg": "found vulnerabilites: Spectre2"}
fatal: [oldgw]: FAILED! => {"changed": false, "failed": true, "msg": "found vulnerabilites: Spectre2"}
```

# References
Red Hat Knowledge article: https://access.redhat.com/security/vulnerabilities/speculativeexecution

What is Spectre and Meltdown: https://www.redhat.com/en/blog/what-are-meltdown-and-spectre-heres-what-you-need-know

# Disclaimer
I wrote this on my own time for my own purposes. This playbook is not official, not endorsed, not supported, nor maintained by Red Hat.
