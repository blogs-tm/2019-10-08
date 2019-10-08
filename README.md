#AnsibleとS3の連携について

## 検証環境

インフラ: AWS

インフラ構成:
[[ CFnの図 ]]

Ansible Control OS:
  AMI Image Id:
  OS Version: CentOS Linux release 7.6.1810 (Core)
  Ansible:
    インストール方法: yum
    version: ansible 2.4.2.0
    other info:
      config file = /etc/ansible/ansible.cfg
      configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
      ansible python module location = /usr/lib/python2.7/site-packages/ansible
      executable location = /bin/ansible
      python version = 2.7.5 (default, Oct 30 2018, 23:45:53) [GCC 4.8.5 20150623 (Red Hat 4.8.5-36)]
  Pip libraries:
Package                          Version
-------------------------------- --------
ansible                          2.4.2.0
Babel                            0.9.6
backports.ssl-match-hostname     3.5.0.1
boto3                            1.9.244
botocore                         1.12.244
cffi                             1.6.0
chardet                          2.2.1
cloud-init                       18.2
configobj                        4.7.2
cryptography                     1.7.2
decorator                        3.4.0
docutils                         0.15.2
enum34                           1.0.4
futures                          3.3.0
httplib2                         0.9.2
idna                             2.4
iniparse                         0.4
ipaddress                        1.0.16
IPy                              0.75
Jinja2                           2.7.2
jmespath                         0.9.0
jsonpatch                        1.2
jsonpointer                      1.9
kitchen                          1.1.1
MarkupSafe                       0.11
paramiko                         2.1.1
passlib                          1.6.5
perf                             0.1
pip                              19.2.3
ply                              3.4
policycoreutils-default-encoding 0.1
prettytable                      0.7.2
pyasn1                           0.1.9
pycparser                        2.14
pycurl                           7.19.0
pygobject                        3.22.0
pygpgme                          0.3
pyliblzma                        0.5.3
pyserial                         2.6
python-dateutil                  2.8.0
python-linux-procfs              0.4.9
pyudev                           0.15
pyxattr                          0.5.1
PyYAML                           3.10
requests                         2.6.0
s3transfer                       0.2.1
schedutils                       0.4
seobject                         0.1
sepolicy                         1.1
setuptools                       0.9.8
six                              1.9.0
urlgrabber                       3.10
urllib3                          1.25.6
yum-metadata-parser              1.1.4

Ansible Target OS: CentOS Linux release 7.6.1810 (Core)

## 検証手順

- AWS S3に検証用のバケットを作成する
- AWS ClouldFormaionからテンプレートを利用してVPCを起動する
- Ansible ControlマシーンにSSH接続して秘密鍵を登録する
- ターゲットのマシンに対してansible-playbookコマンドを実行する
