#Imagen Base
FROM almalinux:8

# Instalar todo en una sola capa para hacerlo lo mas optimizado posible y con yarn v--22x
RUN dnf -y update && \
    dnf -y install curl gcc-c++ make which git && \
    curl -fsSL https://rpm.nodesource.com/setup_22.x | bash - && \
    dnf install -y nodejs && \
    npm install -g yarn && \
    node --version && npm --version && yarn --version && \
    dnf clean all && \
    rm -rf /var/cache/dnf

CMD ["/bin/bash"]