# ansible-meltdown-spectre
Ansible Playbook to run the Red Hat spectre-meltdown check script for CVE-2017-5754 CVE-2017-5753 CVE-2017-5715.

Aka: Spectre and Meltdown Kernel side-channel attacks.

# Usage
1. Set your inventory under [Check]
2. Ensure `ansible_user` variable is **root**
3. Make sure `ScriptUrl` variable is set appropriately.

You can run the playbook like so:

```bash
ansible-playbook -i inventory site.yml
```

Hosts that are vulnerable will show up as "changed", and under the `highlight vulnerabilites` task, you will see what vulnerability they have:

```
ok: [oldgw] => (item=Spectre1)
changed: [oldgw] => (item=Spectre2)
ok: [oldgw] => (item=Meltdown)
```

# References
Red Hat Knowledge article: https://access.redhat.com/security/vulnerabilities/speculativeexecution

What is Spectre and Meltdown: https://www.redhat.com/en/blog/what-are-meltdown-and-spectre-heres-what-you-need-know

# Disclaimer
I wrote this on my own time for my own purposes, this playbook is not official, not endorsed, not supported, nor maintained by Red Hat.
