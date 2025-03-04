# practica-iaw-3.2

En esta practica realizaremos mediante Ansible una instalación en 3 niveles de *Wordpress*, para ello crearemos en **AWS** 5 maquinas:
1. 2 FRONTALES
2. 1 BACKEND
3. 1 BALANCEADOR
4. 1 SERVIDOR NFS

#Inventory
````
[frontend1]
172.31.29.157
[frontend2]
172.31.25.29
[backend]
172.31.30.17
[loadbalancer]
172.31.16.237
[nfs_server]
172.31.24.33

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/ubuntu4.pem
ansible_ssh_common_args='-o StrictHostKeyChecking=accept-new'
````
Los scripts para la instalación siguen los mismos pasos que en la [practica-iaw-1.11](https://github.com/marinaferb92/practica-iaw-1.11)
- Configuracion de la pila LAMP para Frontend y Backen
- Configuracion del balanceador de carga
- Instalación de certificado
- Instalación de la base de datos Wordpress en el Backend
- Desscarga y configuración de Wordpress en los Frontales
- configuracion de servidor NFS y los clientes NFS
- 
Una vez configurado el inventory podremos ejecutar [main.yml]([main.yml](https://github.com/marinaferb92/practica-iaw-3.2/blob/256f167f6713fecf8a3c9a1a2b1cedb64fe481bd/main.yml)), donde tendremos puestos todos los playbooks en el orden de ejcución que queremos, con el comando `ansible-playbook + la ruta de nuestro inmventario + nuesto usuario + nuestra ruta a la clave vockey`, comenzaremos a ejecutar los playbooks.

![image](https://github.com/user-attachments/assets/dbf5d279-538a-466e-9bc1-e9d6c1e21d00)

Al terminar veremos que se han ejecutado todos los cambios sin errores.

![image](https://github.com/user-attachments/assets/f8da878e-46e2-444e-a82c-8e2b47ee12fb)


#COMPROBACIONES
Para comprobar que todo ha funcionado, entraremos en el dominio que hemos definido para la IP del balanceador

![image](https://github.com/user-attachments/assets/3b6b916d-af0e-4ad2-b712-f1957a503d96)

Tambien podemos comprobar si el servidor NFS está funcionando

![image](https://github.com/user-attachments/assets/a94f457d-42e6-48ea-ba7f-ba21d655ad46)

Y con el comando `df -h` podemos ver si los frontales estan correctamente configurados como cliente NFS

![image](https://github.com/user-attachments/assets/ed6f7265-e6c5-47f6-b37f-bf7dd1556608)

Tambien comprobamos que el certificado se ha creado correctamente para nuestro dominio

![image](https://github.com/user-attachments/assets/1f103e4b-dab4-4d79-8448-a5d68399e71d)

