#Imagen Base 
FROM almalinux:8

# Actualizar sistema e instalar dependencias y herramientas para el contenedor.
RUN dnf -y update && \
    dnf -y install \
        git \
        gcc \
        bzip2 \
        openssl-devel \
        libffi-devel \
        readline-devel \
        zlib-devel \
        gdbm-devel \
        ncurses-devel \
        make \
        which \
        redhat-rpm-config

# Instalar rbenv desde git
RUN git clone https://github.com/rbenv/rbenv.git /root/.rbenv

# Entorno para configurar rbenv en el PATH
ENV PATH="/root/.rbenv/bin:/root/.rbenv/shims:${PATH}"

# Instalar ruby-build plugin
RUN git clone https://github.com/rbenv/ruby-build.git /root/.rbenv/plugins/ruby-build

# Inicializar rbenv y instalar Ruby
RUN echo 'eval "$(/root/.rbenv/bin/rbenv init - bash)"' >> /root/.bashrc

# Instalar una versión específica de Ruby
RUN /root/.rbenv/bin/rbenv install 3.1.2 && \
    /root/.rbenv/bin/rbenv global 3.1.2

# Verificar instalación
RUN /root/.rbenv/bin/rbenv versions && \
    /root/.rbenv/shims/ruby --version && \
    /root/.rbenv/shims/gem --version

WORKDIR /app