# README

ansible_localを使ってプロビジョニングするplaybookを作りました。

## 開発環境

VirtualBox5.1.2
Vagrant1.8.6

### OSとミドルウェアのバージョン ※2016-10-24時点

 * centos 7.2
 * Apache 2.4.6
 * PHP 7.0.12
 * mariadb 10.1.18
 * nodejs v6.7.0
 * npm 3.10.3
 * Composer 1.2.1


## 構築手順

ダウンロードする

    $ git clone https://github.com/OsamuKubomoto/ansible_local-centos72lamp.git test-ansible-local

/provision/group_vars/allを適宜修正してください。

ゲストOSを起動

    $ cd test-ansible-local
    $ vagrant up

初回起動時、下記のように共有フォルダのマウントでエラーが起きる場合は、以下の手順で進めます。

    ==> default: Mounting shared folders...
        default: /vagrant => path/to/test-ansible-local
    
    Failed to mount folders in Linux guest. This is usually because
    the "vboxsf" file system is not available. Please verify that
    the guest additions are properly installed in the guest and
    can work properly. The command attempted was:
    
    mount -t vboxsf -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3`,dmode=777,fmode=777 vagrant /vagrant
    mount -t vboxsf -o uid=`id -u vagrant`,gid=`id -g vagrant`,dmode=777,fmode=777 vagrant /vagrant
    
    The error output from the last command was:
    
    /sbin/mount.vboxsf: mounting failed with the error: No such device

ゲストOSのカーネルをアップデートします。

    $ vagrant ssh -c "sudo yum update -y kernel"

ゲストOSを再起動

    $ vagrant reload

