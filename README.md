Role cloud_kvm
==============

Cloud KVM role help you to deploy a CloudInit image domain in Linux KVM.

version: 0.1.0

Requirements
------------

Minimum Ansible 2.8, KVM, libvirt 


Role Variables
--------------

Those variables define class, cidata, image and iso file used to deploy domain for each Linux target.

**TARGET OS - ubuntu, rhel, centos**

    # debian, ubuntu, rhel, fedora, centos
    cloud_os: rhel
    class_os: "{{ CLOUDINIT[cloud_os].class }}"

**Cloud-Init images default dict**

    CLOUDINIT:
      debian:
        class: DEBIAN
        cidata: [ meta-data, user-data ]
        iso: DEBIAN/debian-10.4.0-amd64-netinst.iso
        img: ""
        url: ""
      ubuntu:
        class: DEBIAN
        cidata: [ meta-data, user-data ]
        iso: UBUNTU/ubuntu-20.04-live-server-amd64.iso
        img: focal-server-clouding-amd64.img   # focal5.img
        url: https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64.img
      centos:
        class: REDHAT
        cidata: [ meta-data, user-data ]
        iso: ""
        img: REDHAT/CentOS-8-x86_64-GenericCloud.qcow2
        url: https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.1.1911-20200113.3.x86_64.qcow2
      rhel:
        class: REDHAT
        cidata: [ meta-data, user-data ]
        iso: REDHAT/rhel-8.0-x86_64-dvd.iso
        img: rhel-8.0-update-3-x86_64-kvm.qcow2
        url: file:///mnt/depot/iso/CLOUD/rhel-8.0-update-3-x86_64-kvm.qcow2
      windows:
        class: WINDOWS

Example Playbook
----------------

    - name: CloudInit domain example
      hosts: all
      gather_facts: no
      roles:
        - cloud_kvm

License
-------

Apache 2.0

