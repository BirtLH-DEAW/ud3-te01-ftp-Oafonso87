# Usar la última imagen de Ubuntu
FROM ubuntu:latest

# Actualizar e Instalar Proftpd, Nano y Openssl
RUN apt-get update && apt-get install -y proftpd nano openssl proftpd-mod-crypto

RUN mkdir -p /srv/deaw/Recursos_Contenedor_2

# Crear usuario deaw con contraseña deaw y sin poder loguearse en el sistema
RUN useradd deaw \
    --create-home \
    --home-dir /srv/deaw \
    --password $(openssl passwd -1 deaw) \    
    --shell /usr/sbin/nologin

RUN chown -R deaw:deaw /srv/deaw

# Generar un certificado SSL con OpenSSL
RUN openssl req -new -newkey rsa:4096 -x509 -days 365 -nodes \
    -out /etc/ssl/certs/proftpd.crt \
    -keyout /etc/ssl/private/proftpd.key \
    -subj "/C=ES/ST=Bizkaia/L=Bilbao/O=BirtLH/OU=DEAW/CN=Omar Afonso/emailAddress=oafonso@birt.eus"
  
# Copiar los archivos necesarios
COPY Recursos_Contenedor_2/DefaultRoot_comandos.txt /srv/deaw/Recursos_Contenedor_2
COPY Recursos_Contenedor_2/FTP_comandos.txt /srv/deaw/Recursos_Contenedor_2
COPY Recursos_Contenedor_2/FTPanonimo_comandos.txt /srv/deaw/Recursos_Contenedor_2
COPY Recursos_Contenedor_2/README.txt /srv/deaw/Recursos_Contenedor_2

RUN chown -R deaw:deaw /srv/deaw/Recursos_Contenedor_2/

COPY conf/proftpd.conf /etc/proftpd/proftpd.conf
COPY conf/modules.conf /etc/proftpd/modules.conf
COPY conf/tls.conf /etc/proftpd/tls.conf

# Reiniciar Proftpd para aplicar los cambios
RUN  service proftpd restart

# Exponemos los puertos para el modo pasivo
EXPOSE 21 50000-50030