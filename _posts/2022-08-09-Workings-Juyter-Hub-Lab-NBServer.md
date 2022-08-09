---
layout: post
author: Anish PK
description: High Level Workings of Jupyter Hub, Jupyter Lab and Jupyter Notebook Server
---

## High Level Workings of Jupyter Hub, Jupyter Lab and Jupyter Notebook Server .
<br>
### JupyterHub

[JupyterHub](https://github.com/jupyterhub/jupyterhub) is the best way to serve [Jupyter notebook](https://jupyter-notebook.readthedocs.io/en/latest/) for multiple users. It can be used in a classes of students, a corporate data science group or scientific research group. It is a multi-user Hub that spawns, manages, and proxies multiple instances of the single-user [Jupyter notebook](https://jupyter-notebook.readthedocs.io/en/latest/) server.

Following are the 4 Subsystems that make up the Jupyter Hub

- **Hub (Python/Tornado**): manages user accounts, authentication, and coordinates Single User Notebook Servers using a Spawner.

Note : What is Tornado - [Tornado](https://www.tornadoweb.org/) is a Python web framework and asynchronous networking library, originally developed at [FriendFeed](https://en.wikipedia.org/wiki/FriendFeed). By using non-blocking network I/O, Tornado can scale to tens of thousands of open connections, making it ideal for [long polling](https://en.wikipedia.org/wiki/Push_technology#Long_polling), [WebSockets](https://en.wikipedia.org/wiki/WebSocket), and other applications that require a long-lived connection to each user.

- **Proxy**: the public facing part of JupyterHub that uses a dynamic proxy to route HTTP requests to the Hub and Single User Notebook Servers. configurable http proxy (node-http-proxy) is the default proxy.

Note: Unlike anyother reverse proxy this node-http-proxy has the ability to dynamically create routes when a new user is registered or authenticated.

- multiple single-user **Jupyter notebook servers (Python/IPython/tornado)** that are monitored by Spawners

- an **authentication class** that manages how users can access the system


<img class="img-fluid" src='/assets/images/posts/jupyter/jhub-parts.png' alt="">
<br>
### Jupyter Lab
<br>
Its a typescript and python based application which has many inbuilt features as npm packages.  You can extend the jupyter lab and have custom extensions or use one of the already available extensions.
<br>
### Jupyter NotebookServer ( Single User Notebook Server )
<br>
**A web application**: a browser-based tool for interactive authoring of documents which combine explanatory text, mathematics, computations and their rich media output.

<img src="/assets/images/posts/jupyter/jupyter-interactive.png">


- The user interacts with the browser, consequently, a request is sent to the Notebook server

- If user code has to be executed, the notebook server sends it to the kernel in ZeroMQ messages

- The kernel returns the results of the execution. At last, the notebook server returns an HTML page to the user.

- When the user saves the document, it is sent from the browser to the notebook server. The server saves it on disk as a JSON file with a `.ipynb` extension.

- This notebook file contains the code, output and markdown notes.

<br>
### How the Subsystems Interact
<br>
Users access JupyterHub through a web browser, by going to the IP address or the domain name of the server.

The basic principles of operation are:

- The Hub spawns the proxy (in the default JupyterHub configuration)

- The proxy forwards all requests to the Hub by default

- The Hub handles login, and spawns single-user notebook servers on demand

- The Hub configures the proxy to forward url prefixes to single-user notebook servers


The proxy is the only process that listens on a public interface. The Hub sits behind the proxy at `/hub`. Single-user servers sit behind the proxy at `/user/[username]`.
<br>
#### References :

<sub>https://jupyterhub.readthedocs.io/en/stable/</sub><br>
<sub>https://jupyterhub.readthedocs.io/en/stable/reference/technical-overview.html</sub><br>
<sub>https://jupyterhub.readthedocs.io/en/stable/</sub><br>
<sub>https://www.tornadoweb.org/en/stable/</sub><br>
<sub>https://jupyterlab.readthedocs.io/en/stable/user/interface.html</sub><br>
