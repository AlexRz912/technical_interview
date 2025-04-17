FROM debian:latest

ARG USERNAME=test
ARG USER_UID=1000
ARG USER_GID=1000
ARG USER_PWD=secret

RUN apt-get update && \
    apt-get install -y openssl

RUN ENCRYPTED_PASS=$(openssl passwd -1 "$USER_PWD") && \
    groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -p "$ENCRYPTED_PASS"
