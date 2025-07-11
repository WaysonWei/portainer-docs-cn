# Install Portainer BE with Podman on Linux


These installation instructions are for Portainer Business Edition (BE). For Portainer Community Edition (CE) refer to the [CE install documentation](../../../install-ce/server/podman/linux.md).


## Introduction

Portainer consists of two elements, the _Portainer Server_, and the _Portainer Agent_. Both elements run as lightweight containers on a Podman engine. This document will help you install the Portainer Server container on your Linux environment. To add a new Linux environment to an existing Portainer Server installation, please refer to the [Portainer Agent installation instructions](../../../../admin/environments/add/podman/agent.md).

To get started, you will need:

* CentOS 9 with the latest version of Podman 5.x installed and working on your Podman host. Other Podman versions and Linux distros may work but we currently only support the above. We recommend following the [official installation instructions](https://podman.io/docs/installation#installing-on-linux) for Podman.
* sudo access on the machine that will host your Portainer Server instance
* By default, Portainer Server will expose the UI over port `9443` and expose a TCP tunnel server over port `8000`. The latter is optional and is only required if you plan to use the Edge compute features with Edge agents.
* A license key for Portainer Business Edition.

The installation instructions also make the following assumptions about your environment:

* Your environment meets [our requirements](../../../requirements-and-prerequisites.md). While Portainer may work with other configurations, it may require configuration changes or have limited functionality.
* You are accessing Podman via Unix sockets.
* Podman is running as root. Portainer with rootless Podman may work but is currently not officially supported.

## Deployment

First, ensure the Podman socket is enabled:

```
systemctl enable --now podman.socket
```

Next, create the volume that Portainer Server will use to store its database:

```bash
podman volume create portainer_data
```

Then, download and install the Portainer Server container:

<pre><code><strong>podman run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always --privileged -v /run/podman/podman.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:lts
</strong></code></pre>


By default, Portainer generates and uses a self-signed SSL certificate to secure port `9443`. Alternatively you can provide your own SSL certificate [during installation](../../../../advanced/ssl.md#using-your-own-ssl-certificate-on-docker-standalone) or [via the Portainer UI](../../../../admin/settings/#ssl-certificate) after installation is complete.



If you require HTTP port `9000` open for legacy reasons, add the following to your `podman run` command:

`-p 9000:9000`


Portainer Server has now been installed. You can check to see whether the Portainer Server container has started by running `podman ps`:

```bash
root@server:~# podman ps
CONTAINER ID   IMAGE                          COMMAND                  CREATED       STATUS      PORTS                                                                                  NAMES             
de5b28eb2fa9   portainer/portainer-ee:lts     "/portainer"             2 weeks ago   Up 9 days   0.0.0.0:8000->8000/tcp, :::8000->8000/tcp, 0.0.0.0:9443->9443/tcp, :::9443->9443/tcp   portainer
```

## Logging In

Now that the installation is complete, you can log into your Portainer Server instance by opening a web browser and going to:

```bash
https://localhost:9443
```

Replace `localhost` with the relevant IP address or FQDN if needed, and adjust the port if you changed it earlier.

You will be presented with the initial setup page for Portainer Server.


[setup.md](../setup.md)

