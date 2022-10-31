# 1. First Command

```
ansible-playbook playbooks/dev/main.yml --diff
```
```bash
TASK [docker : install python package manager] ***************************************************************************************************************************************************************************
Enter passphrase for key '/Users/desmigor/.ssh/id_rsa': 
The following additional packages will be installed:
  binutils build-essential cpp cpp-5 dpkg-dev fakeroot g++ g++-5 gcc gcc-5
  libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl
  libasan2 libatomic1 libc-dev-bin libc6-dev libcc1-0 libcilkrts5 libdpkg-perl
  libexpat1-dev libfakeroot libfile-fcntllock-perl libgcc-5-dev libgomp1
  libisl15 libitm1 liblsan0 libmpc3 libmpfr4 libmpx0 libpython3-dev
  libpython3.5-dev libquadmath0 libstdc++-5-dev libtsan0 libubsan0
  linux-libc-dev make manpages manpages-dev python-pip-whl python3-dev
  python3-setuptools python3-wheel python3.5-dev
Suggested packages:
  binutils-doc cpp-doc gcc-5-locales debian-keyring g++-multilib
  g++-5-multilib gcc-5-doc libstdc++6-5-dbg gcc-multilib autoconf automake
  libtool flex bison gdb gcc-doc gcc-5-multilib libgcc1-dbg libgomp1-dbg
  libitm1-dbg libatomic1-dbg libasan2-dbg liblsan0-dbg libtsan0-dbg
  libubsan0-dbg libcilkrts5-dbg libmpx0-dbg libquadmath0-dbg glibc-doc
  libstdc++-5-doc make-doc man-browser python-setuptools-doc
The following NEW packages will be installed:
  binutils build-essential cpp cpp-5 dpkg-dev fakeroot g++ g++-5 gcc gcc-5
  libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl
  libasan2 libatomic1 libc-dev-bin libc6-dev libcc1-0 libcilkrts5 libdpkg-perl
  libexpat1-dev libfakeroot libfile-fcntllock-perl libgcc-5-dev libgomp1
  libisl15 libitm1 liblsan0 libmpc3 libmpfr4 libmpx0 libpython3-dev
  libpython3.5-dev libquadmath0 libstdc++-5-dev libtsan0 libubsan0
  linux-libc-dev make manpages manpages-dev python-pip-whl python3-dev
  python3-pip python3-setuptools python3-wheel python3.5-dev
0 upgraded, 47 newly installed, 0 to remove and 8 not upgraded.
changed: [yacloud-vm]

TASK [docker : install python sdk] ***************************************************************************************************************************************************************************************
changed: [yacloud-vm]

PLAY RECAP ***************************************************************************************************************************************************************************************************************
yacloud-vm                 : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

# 2. Second Command

```bash
ansible-inventory -i inventory/main.yml --list
```
```bash
{
    "_meta": {
        "hostvars": {
            "yacloud-vm": {
                "ansible_become": true,
                "ansible_host": "62.84.113.228",
                "ansible_user": "ubuntu"
            }
        }
    },
    "all": {
        "children": [
            "ungrouped"
        ]
    },
    "ungrouped": {
        "hosts": [
            "yacloud-vm"
        ]
    }
}
```
<br>

# 3. Deploying the app

```
ansible-playbook ./playbooks/dev/app_python.yml
```
## Now accessible on: [http://62.84.113.228:8080/](http://62.84.113.228:8080/)

<br>

```
PLAY [Deploying Python app] ********************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************
ok: [yacloud-vm]

TASK [docker : install prerequisites] **********************************************************************************************************************
ok: [yacloud-vm]

TASK [docker : add apt-key] ********************************************************************************************************************************
ok: [yacloud-vm]

TASK [docker : add docker repo] ****************************************************************************************************************************
ok: [yacloud-vm]

TASK [docker : install docker] *****************************************************************************************************************************
ok: [yacloud-vm]

TASK [docker : add user permissions] ***********************************************************************************************************************
changed: [yacloud-vm]

TASK [docker : Reset ssh connection for changes to take effect] ********************************************************************************************

TASK [docker : install python package manager] *************************************************************************************************************
Enter passphrase for key '/Users/desmigor/.ssh/id_rsa': 
ok: [yacloud-vm]

TASK [docker : install docker python sdk] ******************************************************************************************************************
ok: [yacloud-vm]

TASK [web_app : Wipe] **************************************************************************************************************************************
included: /Users/desmigor/learning-projects/devops-labs/ansible/roles/web_app/tasks/0-wipe.yml for yacloud-vm

TASK [web_app : Stop all Docker services] ******************************************************************************************************************
changed: [yacloud-vm]

TASK [web_app : Remove app content] ************************************************************************************************************************
changed: [yacloud-vm]

TASK [web_app : Start Docker service] **********************************************************************************************************************
ok: [yacloud-vm]

TASK [web_app : Create app directory] **********************************************************************************************************************
changed: [yacloud-vm]

TASK [web_app : Pull app image from Docker registry] *******************************************************************************************************
ok: [yacloud-vm]

TASK [web_app : Template a docker file] ********************************************************************************************************************
changed: [yacloud-vm]

TASK [web_app : Run docker-compose] ************************************************************************************************************************
changed: [yacloud-vm]

PLAY RECAP *************************************************************************************************************************************************
yacloud-vm                 : ok=16   changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```