# root-ansible

This ansible recipe builds root-cern.

## Run

Build root-cern on the host machine running the following command from the repo directory:

    ansible-playbook -i inventory/hosts.yml local-root-cern.yml --ask-sudo-pass -vvvv

## Requirements

This playbook requires that the host machine has ansible v2.2, since the argument `remote_src` of the module `unarchive` was not present before.

It may be possible to install root-cern on some guest machines by changing the inventory. Te requirements would then be having ansible v2.2 installed on the host machine and having an ssh connection to the guest machines.

## Details

This playbook configures root-cern with cmake and then compiles it with make. Every prerequisite is installed in the early stages of the playbook, so a user with administrative privileges is required.

root-cern is not installed system-wide, but locally, in `~/software/root/root-${version}-install`. 

In order to make the system aware of the installation, at the end of the playbook the `thisroot.sh` sourcing is added into `~/.bashrc`. In order to use root you need either to `source ~/.bashrc` or to open a new bash terminal. 

If you use another shell, you have to source the `thisroot.sh`, but I guess that you know how to do it.

## Troubleshoot

I have not tested it yet on a centos7 machine, so it be that it does not work there, even though i copied the package names from https://root.cern.ch/build-prerequisites

## Further improvements

The `local.yml` file is not so nice, so it may undergo some refactoring.

## Pull Requests

Any meaningfull pull request is much appreciated!
