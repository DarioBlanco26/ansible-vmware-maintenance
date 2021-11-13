# ansible-vmware-maintenance 

Proyecto para scripts referentes a trabajos de mantenimiento VMWARE

## **Descripción:**
Playbook de ansible para mantenimiento Vmware

Utilizado para establecer en mantenimiento nodos del vcenter:
* Apagado de servidores masivos
* Encendido de servidores masivos

## **Configuración de Inventario**

El inventario esta conformado por 3 secciones especificas:


__VMWARE:__ Utilizado para indicar el nombre de las maquinas virtuales

__LINUX:__ Utilizado para indicar el nombre de la vm y la ip o host correspondiente del servidor linux

__WINDOWS:__ Utilizado para indicar el nombre de la vm y la ip o host correspondiente del servidor windows


> Si se necesita hacer un apagado/encendido desde el vcenter, debe de indicar los servidores en el grupo `[VM]`

__formato:__
* TEST-RHEL-DUMMY-LAB01

> Si se necesita hacer un apagado/encendido desde el host linux `(shutdown -h now)`, debe de especificar los servidores en el grupo `[linux_server]`

__formato:__
* TEST-RHEL-DUMMY-LAB01 ansible_host=tl-dummy-lab01
* TEST-RHEL-DUMMY-LAB01 ansible_host=10.10.15.33

## **Lanzar Playbook**

El playbook utiliza una variable para indicar el estado de la VM

```yaml
state: on | off
```

Utilice el plkaybook principal de la siguiente forma:

En el servidor ansible, con el usuario ansible, ir a 

```
./ansible-vmware-maintenance
```

Apagar de forma masiva
```
ansible-playbook playbook.yml -i inventory/hosts -e "state=off" 
```

Encender de forma masiva
```
ansible-playbook playbook.yml -i inventory/hosts -e "state=on" 
```

Apagar/Encender un servidor especifico
```
ansible-playbook playbook.yml -i inventory/hosts -e "state=off" --limit=TEST-RHEL-DUMMY-LAB01
ansible-playbook playbook.yml -i inventory/hosts -e "state=on" --limit=TEST-RHEL-DUMMY-LAB01
```
