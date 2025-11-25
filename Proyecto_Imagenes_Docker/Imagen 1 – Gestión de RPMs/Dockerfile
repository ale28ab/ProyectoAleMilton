#Imagen Base 
FROM almalinux:8

# Instalacion de dependencias en una sola capa para poder crear el repositorio y optimizar 
RUN dnf -y update && \
    dnf -y install \
        rpm-build rpmdevtools dnf-utils createrepo_c \
        gcc make wget curl tar gzip sudo git spectool rpmlint && \
    dnf clean all && \
    rm -rf /var/cache/dnf

# Configurar usuario y entorno y otorga permisos sudo sin contraseñas
RUN useradd -m rpmuser && \
    echo "rpmuser ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    chmod 440 /etc/sudoers

USER rpmuser
WORKDIR /home/rpmuser

# Configuracion del entorno y estructura
RUN rpmdev-setuptree && \
    mkdir -p scripts sources && \
    echo 'alias ll="ls -la"' >> ~/.bashrc && \
    echo 'export PS1="[\u@rpm-builder \W]\\$ "' >> ~/.bashrc

#Establece directorio home como directorio de trabajo
ENV HOME=/home/rpmuser \ 
    RPM_BUILD_DIR=/home/rpmuser/rpmbuild

WORKDIR $RPM_BUILD_DIR

#Se encarga de iniciar una shell bash cuando se ejecute el contenedor.
CMD ["/bin/bash"]