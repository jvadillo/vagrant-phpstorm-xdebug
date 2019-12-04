# vagrant-phpstorm-xdebug
Configuración paso a paso del entorno de desarollo con Vagrant y PhpStorm.
La máquina virtual está preparada como servidor LAMP (Linux, Apache, MySQL, PHP).


## Pasos

### 1. Configuración de entorno ([videotutorial](https://www.youtube.com/watch?v=DxA-YXbKfiY&t=272s]))
1. Descargar e instalar [VirtualBox](https://www.virtualbox.org/).
2. Descargar e instalar [Vagrant](https://www.vagrantup.com/).
3. Crear fichero de configuración de Vagrant en el directorio del proyecto.
4. Crear script de instalación del entorno (PHP + Apache + MySQL + Xdebug).

### 2. Configuración de PhpStorm ([videotutorial](https://www.youtube.com/watch?v=jEkldlxIOiE]))
1. Configurar PhpStorm

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


