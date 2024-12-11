# Usar la última imagen de Ubuntu
FROM ubuntu:latest

# Actualizar e Instalar Proftpd y Nano
RUN apt-get update && apt-get install -y proftpd nano
RUN mkdir -p /srv/ftp/Recursos_Contenedor_1/css_index

# Copiar los archivos necesarios
COPY Recursos_Contenedor_1/index.html /srv/ftp/Recursos_Contenedor_1
COPY Recursos_Contenedor_1/css_index/style.css /srv/ftp/Recursos_Contenedor_1/css_index
COPY Recursos_Contenedor_1/css_index/demo.css /srv/ftp/Recursos_Contenedor_1/css_index

COPY conf/proftpd.conf /etc/proftpd/proftpd.conf

# Reiniciar Proftpd para aplicar los cambios
RUN service proftpd restart

# Exponemos los puertos para el modo pasivo
EXPOSE 21 50000-50030