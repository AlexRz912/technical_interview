# How to use this tool ? 

    These are the versions of the different dependencies used throughout the development of this tool.

    ```
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
    ```

    



# Why did I decide not to switch to latest docker version

    Since docker offer multiple dependencies, these dependencies need to work together, I'm not particularily proficient with docker so I decided not to upgrade.
    I've also noticed that no bug fixing on the latest version seemed to be related to any security issue -> see 2.35.0 : https://docs.docker.com/compose/releases/release-notes/
