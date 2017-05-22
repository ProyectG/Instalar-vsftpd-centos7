# Instalar-vsftpd-centos7
Instalar un ftp en centos 7.

Requerimientos:
- Maquina con Centos 7
- Editor de texto

Pasos:

- 1: Instalar el editor de texto: yum install nano
- 2: Instalar el vsftpd: yum install vsftpd
- 3: Editar vsftpd.conf: nano /etc/vsftpd/vsftpd.conf
  - Editar las siguientes lineas:
     - anonymous_enable=NO
     - chroot_local=YES (si quieres enjaular a tus usuarios, No si se pueden mover libremente)
- 4: Crear usuario: useradd tu_usuario, luego passwd tu_usuario, te pedira la contraseña
- 5: Habilitar el puerto de firewall: firewall-cmd --zone=public --port=21/tcp
- 6: Cambiar el selinux de centos que es demasiado agresivo:
  - nano /etc/sysconfig/selinux
  - cambiar la linea LINUX=enforcing a LINUX=permissive, si no te permite crear carpetas o ver  desabilitarlo disabled
- 7: Reiniciar la maquina
- 8: habilitarel servicio ftp: systemctl start vsftpd
- 9: Conectarse y usar tu ftp.

Extras:

#Conectarse como root

- 1: Modificar el vsftpd.conf (mirar linea 3):
  - Modificar userlist_enable=YES
  - nano /etc/vsftpd/ftpusers y comentar el root "#root"
  - nano /etc/vsftpd/user_list y comentar root "#root"
- 2: Reiniciar vsftpd: systemctl restart vsftpd

#No se recomienda usar root para usarlo como ftp.
