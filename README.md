# vagrant-phpstorm-xdebug
Configuración paso a paso del entorno de desarollo con Vagrant y PhpStorm.
La máquina virtual está preparada como servidor LAMP (Linux, Apache, MySQL, PHP).


## Pasos

### 1. Configuración de entorno ([videotutorial](https://www.youtube.com/watch?v=DxA-YXbKfiY&t=272s]))
1. Descargar e instalar [VirtualBox](https://www.virtualbox.org/).
2. Descargar e instalar [Vagrant](https://www.vagrantup.com/).
3. Crear fichero de configuración de Vagrant en el directorio del proyecto.
4. Crear script de instalación del entorno (PHP + Apache + MySQL + Xdebug).

### 2a. Configuración de PhpStorm ([videotutorial](https://www.youtube.com/watch?v=jEkldlxIOiE]))
Configurar PhpStorm siguiendo los pasos del videotutorial.

### 2b. Configuración de VS Code
En caso de utilizar VS Code, recomendamos configurar el IDE de la siguiente forma:
- Instala la extensión PHP Intelephense
- Deshabilita las opciones de PHP que vienen por defecto. Para ello busca "@builtin php" en el buscador de extensiones y deshabilítalo.
- Si quieres abrir tus archivos .php en el navegador desde VS Code, puedes hacerlo instalando la extensión Open PHP/HTML/JS In Browser. Una vez hecho, para que al abrir los archivos .php lo haga utilizando el servidor de Vagrant, tendrás que ir a `Settings > Extensions > Open PHP/HTML/JS In Browser` y establecer el Custom Host (con el valor `localhost:8765` en nuestro caso) y Custom URL to open (con el valor `http://${host}/${relativeDirnameDocumentRoot}/${relativeFile}`).

## Extras
### Habilitar acceso a Internet a la máquina
En caso de necesitar acceso a Internet desde la máquina virtual, añadir lo siguiente al Vagrantfile:
```
config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
end
```
Esto puede ser necesario por ejemplo si quieres instalar paquetes mediante composer.

### Mostrar errores de PHP
Es recomendable activar la opción que permite visualizar los errores de PHP durante el desarrollo. Para ello la forma más sencilla es modificar el archivo `php.ini` ubicado en la ruta `/etc/php/7.2/apache2/`. Sigue los siguientes pasos:

1. Acceder a la máquina virtual mediante el comando `vagrant ssh`
2. Abrir el fichero con un editor, por ejemplo, Nano: 
```
sudo nano /etc/php/7.2/apache2/php.ini
```
3. Buscar la propiedad `display_errors` (puedes emprear el comando CTRL+W) y establecer su valor a On.
```
display_errors = On
```
4. Guardar los cambios y reiniciar el servidor Apache:
```
sudo service apache2 restart
```

### Restablecer contraseña en MySQL
En caso de tener problemas para acceder, seguir los siguientes pasos:

1. Parar el servicio: `sudo service mysql stop`
2. Iniciar el servicio: `sudo service mysql start`
3. Restablecer contraseña: `sudo mysql -u root --password="" -e "update mysql.user set authentication_string=password(''), plugin='mysql_native_password' where user='root';"  `
4. Ejecutar `sudo mysql -u root --password="" -e "flush privileges;"`

Ahora ya podrás acceder a la base de datos como root.


