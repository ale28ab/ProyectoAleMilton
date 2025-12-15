#Imagen Base para la imagen
FROM almalinux:8

#Entrono de desarrollo para las variables
ENV NVM_DIR=/root/.nvm \
    RBENV_ROOT=/root/.rbenv

# Se instalan todos los paquetes y herramientas en una sola capa
RUN dnf -y update && \
    dnf -y install \
        rpm-build rpmdevtools dnf-utils createrepo gcc make \
        wget curl tar gzip vim sudo git bzip2 openssl-devel \
        libffi-devel readline-devel zlib-devel python3 python3-pip \
        python3-virtualenv python3-setuptools python3-devel gcc-c++ \
        which findutils && \
    dnf clean all && \
    rm -rf /var/cache/dnf

# Se instala rbenv, Ruby, NVM and Node.js en una sola capa
RUN git clone https://github.com/rbenv/rbenv.git ${RBENV_ROOT} && \
    git clone https://github.com/rbenv/ruby-build.git ${RBENV_ROOT}/plugins/ruby-build && \
    ${RBENV_ROOT}/plugins/ruby-build/install.sh && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash && \
    source $NVM_DIR/nvm.sh && \
    nvm install 16 && \
    nvm install 22 && \
    nvm alias default 22 && \
    npm install -g yarn

# 3.Se configura el ambiente y se crea el usaurio en una sola capa
RUN echo 'export PATH="${RBENV_ROOT}/bin:${RBENV_ROOT}/shims:$PATH"' >> ~/.bashrc && \
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc && \
    echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc && \
    echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc && \
    echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"' >> ~/.bashrc && \
    useradd -m -s /bin/bash rpmuser && \
    echo "rpmuser ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    cp -r /root/.rbenv /home/rpmuser/ && \
    cp -r /root/.nvm /home/rpmuser/ && \
    chown -R rpmuser:rpmuser /home/rpmuser/.rbenv /home/rpmuser/.nvm

# Arranque y configuracion de ambiente rpmuser
USER rpmuser
WORKDIR /home/rpmuser

RUN echo 'export RBENV_ROOT="/home/rpmuser/.rbenv"' >> ~/.bashrc && \
    echo 'export PATH="$RBENV_ROOT/bin:$PATH"' >> ~/.bashrc && \
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc && \
    echo 'export NVM_DIR="/home/rpmuser/.nvm"' >> ~/.bashrc && \
    echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc && \
    echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"' >> ~/.bashrc && \
    rpmdev-setuptree

WORKDIR /home/rpmuser/rpmbuild

CMD ["/bin/bash"]