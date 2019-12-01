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

## Nota
En caso de necesitar acceso a Internet desde la máquina virtual, añadir lo siguiente al Vagrantfile:
```
config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
end
```
Esto puede ser necesario por ejemplo si quieres instalar paquetes mediante composer.


