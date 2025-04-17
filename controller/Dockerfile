FROM almalinux:latest

RUN dnf update -y && \
    dnf install -y epel-release && \
    dnf install ansible -y && \
    ansible --version \  
COPY nginx.yml /etc/ansible
WORKDIR /etc/ansible
ENTRYPOINT ["sleep"]
CMD ["infinity"]
