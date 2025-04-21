FROM almalinux:latest

RUN dnf update -y && \
    dnf install -y epel-release && \
    dnf install -y ansible openssh-clients

# Créer le répertoire pour les clés SSH
RUN mkdir -p /etc/ansible/ssh

COPY nginx.yml /etc/ansible/
COPY inventory /etc/ansible/
COPY ./ssh/id_rsa /etc/ansible/ssh/
COPY ansible.cfg /etc/ansible/ansible.cfg

WORKDIR /etc/ansible

# Définir les bonnes permissions pour la clé SSH
RUN chmod 600 /etc/ansible/ssh/id_rsa

CMD ["/bin/bash", "-c", "ansible-playbook -i inventory nginx.yml"]
