#Imagen Base para la imagen
FROM almalinux:8
#Instalar todo en una sola capa para hacerlo lo mas optimizado posible
RUN dnf -y update && \
    dnf -y install python3 python3-pip && \
    dnf clean all && \
    rm -rf /var/cache/dnf

WORKDIR /app

CMD ["python3"]