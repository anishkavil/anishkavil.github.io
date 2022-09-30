---
layout: post
author: Anish PK
description: High Level Workings of Jupyter Hub, Jupyter Lab and Jupyter Notebook Server
---

## High Level Workings of Jupyter Hub, Jupyter Lab and Jupyter Notebook Server .
<br>

### JupyterHub

[JupyterHub](https://github.com/jupyterhub/jupyterhub) is the best way to serve [Jupyter notebook](https://jupyter-notebook.readthedocs.io/en/latest/) for multiple users. It can be used in a classes of students, a corporate data science group or scientific research group. It is a multi-user Hub that spawns, manages, and proxies multiple instances of the single-user [Jupyter notebook](https://jupyter-notebook.readthedocs.io/en/latest/) server.

Following are the 4 Subsystems that make up the Jupyter Hub

- **Hub (Python/Tornado**): manages user accounts, authentication, and coordinates Single User Notebook Servers using a Spawner.
Note : What is Tornado -[Tornado](https://www.tornadoweb.org/) is a Python web framework and asynchronous networking library, originally developed at [FriendFeed](https://en.wikipedia.org/wiki/FriendFeed). By using non-blocking network I/O, Tornado can scale to tens of thousands of open connections, making it ideal for [long polling](https://en.wikipedia.org/wiki/Push_technology#Long_polling), [WebSockets](https://en.wikipedia.org/wiki/WebSocket), and other applications that require a long-lived connection to each user.
- **Proxy**: the public facing part of JupyterHub that uses a dynamic proxy to route HTTP requests to the Hub and Single User Notebook Servers. configurable http proxy (node-http-proxy) is the default proxy.

Note: Unlike anyother reverse proxy this node-http-proxy has the ability to dynamically create routes when a new user is registered or authenticated.

- multiple single-user **Jupyter notebook servers (Python/IPython/tornado)** that are monitored by Spawners
- an **authentication class** that manages how users can access the system

<img class="img-fluid" src='/assets/images/posts/jupyter/jhub-parts.png' alt="">
<br>

### Jupyter Lab

<br>
Its a typescript and python based application which has many inbuilt features as npm packages.  You can extend the jupyter lab and have custom extensions or use one of the already available extensions.
<br>

### Jupyter NotebookServer ( Single User Notebook Server )

**A web application**: a browser-based tool for interactive authoring of documents which combine explanatory text, mathematics, computations and their rich media output.

<img src="/assets/images/posts/jupyter/jupyter-interactive.png">

- The user interacts with the browser, consequently, a request is sent to the Notebook server
- If user code has to be executed, the notebook server sends it to the kernel in ZeroMQ messages
- The kernel returns the results of the execution. At last, the notebook server returns an HTML page to the user.
- When the user saves the document, it is sent from the browser to the notebook server. The server saves it on disk as a JSON file with a `.ipynb` extension.
- This notebook file contains the code, output and markdown notes.

### How the Subsystems Interact

<br>
Users access JupyterHub through a web browser, by going to the IP address or the domain name of the server.

The basic principles of operation are:

- The Hub spawns the proxy (in the default JupyterHub configuration)
- The proxy forwards all requests to the Hub by default
- The Hub handles login, and spawns single-user notebook servers on demand
- The Hub configures the proxy to forward url prefixes to single-user notebook servers


The proxy is the only process that listens on a public interface. The Hub sits behind the proxy at `/hub`. Single-user servers sit behind the proxy at `/user/[username]`.
<br>

### Jupyter Working 

- Login data is handed to the [Authenticator](https://jupyterhub.readthedocs.io/en/0.7.2/howitworks.html#authentication) instance for validation
- The Authenticator returns the username, if login information is valid
- A single-user server instance is [Spawned](https://jupyterhub.readthedocs.io/en/0.7.2/howitworks.html#spawning) for the logged-in user
- When the server starts, the proxy is notified to forward /user/\[username\]/* to the single-user server
- Two cookies are set, one for /hub/ and another for /user/\[username\], containing an encrypted token.
- The browser is redirected to /user/\[username\], which is handled by the single-user server

CMD+Z to see  what was the command executed behind the form.


### JUPYTER HUB

The Process from JupyterHub Access to User Login. When a user accesses JupyterHub, the following events take place:

- Login data is handed to the Authenticator instance for validation 
- The Authenticator returns the username if the login information is valid 
- A single-user notebook server instance is spawned for the logged-in user 
- When the single-user notebook server starts, the proxy is notified  to forward requests to /user/\[username\]/* to the single-user
notebook server. 
- A cookie is set on /hub/, containing an encrypted token. (Prior to  version 0.8, a cookie for /user/\[username\] was used too.)
- The browser is redirected to /user/\[username\], and the request is  handled by the single-user notebook server. 
- The single-user server identifies the user with the Hub via OAuth:
- on request, the single-user server checks a cookie 
- if no cookie is set, redirect to the Hub for verification via OAuth 
- after verification at the Hub, the browser is redirected back to the  single-user server 
- the token is verified and stored in a cookie 
- if no user is identified, the browser is redirected back to /hub/login  Default Behavior

- By default, the Proxy listens on all public interfaces on port 8000. Thus you can reach JupyterHub through either:
- http://localhost:8000 or any other public IP or domain pointing to your system.

- In their default configuration, the other services, the Hub and Single- User Notebook Servers, all communicate with each other on localhost only.
By default, starting JupyterHub will write two files to disk in the current working directory:
- jupyterhub.sqlite is the SQLite database containing all of the state of the Hub. This file allows the Hub to remember which users are running and where, as well as storing other information enabling you to restart parts of JupyterHub separately. It is important to note that this database contains no sensitive information other than Hub usernames. 
- jupyterhub\_cookie\_secret is the encryption key used for securing cookies. This file needs to persist so that a Hub server restart will avoid invalidating cookies. Conversely, deleting this file and restarting the server effectively invalidates all login cookies. The cookie secret file is discussed in the Cookie Secret section of the Security Settings document.

- The location of these files can be specified via configuration settings. It is recommended that these files be stored in standard UNIX filesystem locations, such as /etc/jupyterhub for all configuration files and /srv/jupyterhub for all security and runtime files.

Docker CMD
Using jupyter notebook as a Docker CMD results in kernels repeatedly crashing, likely due to a lack of PID reaping. To avoid this, use the tini init as your Dockerfile *ENTRYPOINT*:
\# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
\# kernel crashes.
```html
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/$ {TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT \["/usr/bin/tini", "--"\]
EXPOSE 8888
CMD \["jupyter", "notebook", "--port=8888", "--no-browser", "-- ip=0.0.0.0"\]

```

#### References :

> https://jupyterhub.readthedocs.io/en/stable/  
> https://jupyterhub.readthedocs.io/en/stable/reference/technical-overview.html  
> https://jupyterhub.readthedocs.io/en/stable/</sub><br>  
> https://www.tornadoweb.org/en/stable/  
> https://jupyterlab.readthedocs.io/en/stable/user/interface.html</sub><br>
