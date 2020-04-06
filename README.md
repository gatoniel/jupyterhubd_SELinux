# jupyterhubd_SELinux
SELinux Policies for a JupyterHub Daemon

These policies are written for a JupyterHub instance that is started by systemd. The JupyterHub process then does not run as unconfined_service_t, but as jupyterhubd_t domain.

This repo contains the type enforcing file to compile a SELinux module for the domain jupyterhubd_t. It also contains example service files for JupyterHub and configurable-http-proxy (CHP) in a Podman container started by systemd.

This repo was developed on CentOS 8. For other distributions one might need some changes to the files. It uses the targeted version of SELinux on CentOS 8.

## Installation

You need to have SELinux on your machine. In order to easily compile the module you need the Makefile for your distro. On CentOS 8 you can install it via the *selinux-policy-devel* package.

```
sudo dnf -y install selinux-policy-devel
```

Clone this repository into your homedirectory on the machine running JupyterHub. Change directory into the repos jupyterhubd directory. Then copy the Makefile; on CentOS 8, you can find the Makefile under /usr/share/selinux/devel/Makefile, when *selinux-policy-devel* is installed.

```
cp /usr/share/selinux/devel/Makefile .
```

Run `make` to create the corresponding files. A file jupyterhud.pp is now created in the directory. With

```
sudo semodule -i myjupyterhubd.pp
```

the module gets activated; this command takes up to a minute to complete. You could alsp copy the .pp-file into your SELinux module dir and reload SELinux policies.

## Useful ressources
* https://wiki.gentoo.org/wiki/SELinux/Tutorials
* http://seedit.sourceforge.net/doc/access_vectors/

