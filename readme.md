# Why is this readme in english ?
The instructions given to me were in english. Even tho my primary langage is French, it feels more comfortable to answer this in english.

# Docker dependencies versions

These are the versions of the different docker dependencies used.

    
    Client: Docker Engine - Community
        Version:           28.0.4
        API version:       1.48
        Go version:        go1.23.7
        Git commit:        b8034c0
        Built:             Tue Mar 25 15:07:22 2025
        OS/Arch:           linux/amd64
        Context:           default

    Server: Docker Engine - Community
    Engine:
        Version:          28.0.4
        API version:      1.48 (minimum version 1.24)
        Go version:       go1.23.7
        Git commit:       6430e49
        Built:            Tue Mar 25 15:07:22 2025
        OS/Arch:          linux/amd64
        Experimental:     false
    containerd:
        Version:          1.7.27
        GitCommit:        05044ec0a9a75232cad458027ca83437aae3f4da
    runc:
        Version:          1.2.5
        GitCommit:        v1.2.5-0-g59923ef
    docker-init:
        Version:          0.19.0
        GitCommit:        de40ad0

    Docker Compose version v2.34.0
    

# Instructions to create and connect to the ssh-server

Create an ssh key using ssh-keygen and store it into ssh_server folder with file name "ssh".
    
        mkdir ./ssh_server/ssh && \
        mkdir ./controller/ssh && \
        ssh-keygen -t rsa -b 4096
    

Copy key into controller folder in order to use it.
    `cp -r ssh_server/ssh controller/`
(This surely could have been done using volumes, so as not to create a duplicate like this.)

The encryption algorithm doesn't have to be rsa.

Commands to build and run the containers from the command file:

docker compose up --build && docker exec --it ansible /bin/bash`

# Interesting things

I've decided I would go with baby steps, creating one dockerfile, building and running a single container, then moving on to compose.yaml.

Earlier this year, I've had a discussion with a sysadmin that told me : "When a new user (employee) 
is created on a machine, his credentials are given via a post-it note and then the employee gets asked to immediately modify the 
password.". 
I initially thought I should create a secure password and find a secure way to give this password. 
Well, there's a better idea which is to let the user create his password since the ssh server is not created before first usage, and use gitignore
to not push any ssh key to github.

> Question : How would the sysadmin retrieve the credentials in this specific case ? Is it necessary ?
    
I've changed ssh_server hostname to "ssh-server" because I've seen that underscores were not RFC compliant
Here's the actual doc. TL;DR — what I’m saying should be taken with a pinch of salt. -> https://datatracker.ietf.org/doc/rfc1123/

I'm using FQCNs instead of short module name. -> https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html

I failed on the very last step, too little time and prior knowledge regarding ansible, I did ping the ssh server from the ansible controller 
as I used `ENTRYPOINT=["sleep"]` and `CMD=["infinity"]` for debugging purposes.

# Why did I decide not to switch to latest docker version

Since docker offer multiple dependencies, these dependencies need to work together, I'm not particularily proficient with docker so I decided not to upgrade.
I've also noticed that no bug fixing on the latest version seemed to be related to any security issue -> see 2.35.0 : https://docs.docker.com/compose/releases/release-notes/
