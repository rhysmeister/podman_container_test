# containers.podman.podman_container test

The intention of this playbook is to discover the behaviour of the [containers.podman.podman_container](https://docs.ansible.com/ansible/latest/collections/containers/podman/podman_container_module.html) Ansible module in relation to its systemd features.

From this playbook it can be determined that...

* The module does not enable or start a systemd service when it creates it.
* The module restarts the systemd service when the container image is updated.
* The module does not restart the systemd service when the container config is changed.
  * This has only currently been tested with the "ports" parameter.
  * systemd daemon-reload is necessary.
* The module does not restart the systemd service when the systemd config is changed.
  * Evident from the systemd module parameter.
  * systemd daemon-reload is necessary to load a system setting change.

# Running the setup

* Requirements
  * [Vagrant 2.4.1](https://www.vagrantup.com/)
  * [Virtualbox 7+](https://www.virtualbox.org/)
  * [Ansible 2.17.1](https://docs.ansible.com/ansible/latest/index.html)

To execute the setup

```bash
vagrant up
```

To destroy the current instance...

```bash
vagrant destroy
```

# Sample output

This output demonstrates the happy case...

```text
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'rockylinux/9'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'rockylinux/9' version '4.0.0' is up to date...
==> default: Setting the name of the VM: podman_container_test_default_1728843053201_21166
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default:
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default:
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Setting hostname...
==> default: Mounting shared folders...
    default: /vagrant => /Users/rhyscampbell/Documents/git/podman_container_test
==> default: Running provisioner: ansible...
Vagrant gathered an unknown Ansible version:


and falls back on the compatibility mode '1.8'.

Alternatively, the compatibility mode can be specified in your Vagrantfile:
https://www.vagrantup.com/docs/provisioning/ansible_common.html#compatibility_mode

    default: Running ansible-playbook...
 _________________________________________________________
/ PLAY [Setup Podman and container using podman_container \
\ with systemd]                                           /
 ---------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

 ________________________
< TASK [Gathering Facts] >
 ------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

[WARNING]: Platform linux on host default is using the discovered Python
interpreter at /usr/bin/python3.9, but future installation of another Python
interpreter could change the meaning of that path. See
https://docs.ansible.com/ansible-
core/2.17/reference_appendices/interpreter_discovery.html for more information.
ok: [default]
 _______________________
< TASK [Install Podman] >
 -----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [default]
 ______________________________________________________
< TASK [Create and run container with systemd service] >
 ------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [default]
 ________________________________________________________
< TASK [Ensure container service is enabled and started] >
 --------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [default]
 ______________________________
< TASK [ansible.builtin.pause] >
 ------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

Pausing for 30 seconds
ok: [default]
 ________________________________
< TASK [Has my service started?] >
 --------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ________________________________________
< TASK [Check what container is running] >
 ----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 _________________________________________________________
< TASK [Scrape localhost URL and check for specific text] >
 ---------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 ________________________________________________________
/ TASK [Verify the Nginx web server installation text is \
\ present]                                               /
 --------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ___________________________
< TASK [Prefetch container] >
 ---------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [default]
 ___________________________________
< TASK [Change the container image] >
 -----------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ______________
< TASK [pause] >
 --------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

Pausing for 10 seconds
ok: [default]
 __________________________________
< TASK [Has my service restarted?] >
 ----------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ________________________________________
< TASK [Check what container is running] >
 ----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 _________________________________________________________
< TASK [Scrape localhost URL and check for specific text] >
 ---------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 ________________________________________________________
/ TASK [Verify the Nginx web server installation text is \
\ present]                                               /
 --------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ________________________
< TASK [Change the port] >
 ------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [default]
 ___________________________________________________________
< TASK [On this occassion we need to issue a daemon-reload] >
 -----------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ______________________________
< TASK [ansible.builtin.pause] >
 ------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

Pausing for 10 seconds
ok: [default]
 ________________________________________
< TASK [Check what container is running] >
 ----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 _________________________________________________________
< TASK [Scrape localhost URL and check for specific text] >
 ---------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 ________________________________________________________
/ TASK [Verify the Nginx web server installation text is \
\ present]                                               /
 --------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 _______________________________________
< TASK [Change a systemd config option] >
 ---------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [default]
 ________________________________________
< TASK [Check stop timeout is old value] >
 ----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ___________________________________________________________
< TASK [On this occassion we need to issue a daemon-reload] >
 -----------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 ________________________________________
< TASK [Check stop timeout is new value] >
 ----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ________________________________________
< TASK [Check what container is running] >
 ----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 _______________________________
< TASK [ansible.builtin.assert] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 _________________________________________________________
< TASK [Scrape localhost URL and check for specific text] >
 ---------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default]
 ________________________________________________________
/ TASK [Verify the Nginx web server installation text is \
\ present]                                               /
 --------------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [default] => {
    "changed": false,
    "msg": "All assertions passed"
}
 ____________
< PLAY RECAP >
 ------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

default                    : ok=39   changed=7    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```