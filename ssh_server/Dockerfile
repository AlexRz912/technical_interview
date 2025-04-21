FROM debian:latest

ARG USERNAME=test
ARG USER_UID=1000
ARG USER_GID=1000

RUN apt-get update && \
    apt-get install -y openssh-server sudo && \
    mkdir -p /run/sshd

RUN groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -m $USERNAME && \
    mkdir -p /home/$USERNAME/.ssh && \
    chown -R $USERNAME:$USERNAME /home/$USERNAME/.ssh && \
    chmod 700 /home/$USERNAME/.ssh


RUN echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config && \
    sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config

COPY ./ssh/id_rsa.pub /home/$USERNAME/.ssh/authorized_keys

RUN chown $USERNAME:$USERNAME /home/$USERNAME/.ssh/authorized_keys && \
    chmod 600 /home/$USERNAME/.ssh/authorized_keys

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]