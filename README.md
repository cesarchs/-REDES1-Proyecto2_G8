# Proyecto 2 Grupo #8

Para este proyect se tendrá de manera física 3 computadoras conectadas a la VPN formando una pequeña red donde estas tienen conexión y acceso a propiedades de red tradicionales como archivos compartidos por defecto.
Este contará con tres topologías las cuales se describirán a continuación:


# Topología 1
![](https://github.com/cesarchs/-REDES1-Proyecto2_G8/blob/main/imgs/topo1.jpeg)

## RED: 10.8.0.0/16
| Decimal | Binario   | Conversión |
| ------- | --------- | ---------- |
| 10      | 0000 1010 | 8+2 = 10   |
| 8       | 0000 1000 | 8 = 8      |
| 0       | 0000 0000 | 0 = 0      |
| 0       | 0000 0000 | 0 = 0      |

| Red               | Host              |
| ----------------- | ----------------- |
| 00001010 00001000 | 00000000 00000000 |

## Cálculo de subnetting mediante VLSM

#### Subred 1-6

1. Identificar máscara actual: 11111111.11111111.00000000.00000000
2. Obtener número de host: 2^31 = 8192 >= 8192; n = 13
3. Obtener nueva máscara: 11111111.11111111.11111111.11111000 (/29)
4. Obtener salto de red: 256 - 248 = 8

| Salto | Network   | Mask            | P.D asignable | U.D asignable | Broadcast | Host totales | Cantidad de host |
| :---: | --------- | --------------- | ------------- | ------------- | --------- | :----------: | :--------------: |
|   6   | 10.8.0.0  | 255.255.255.248 | 10.8.0.1      | 10.8.0.6      | 10.8.0.7  |      8       |        6         |
|   6   | 10.8.0.8  | 255.255.255.248 | 10.8.0.9      | 10.8.0.14     | 10.8.0.15 |      8       |        6         |
|   6   | 10.8.0.16 | 255.255.255.248 | 10.8.0.17     | 10.8.0.22     | 10.8.0.23 |      8       |        6         |
|   6   | 10.8.0.24 | 255.255.255.248 | 10.8.0.25     | 10.8.0.30     | 10.8.0.31 |      8       |        6         |
|   6   | 10.8.0.32 | 255.255.255.248 | 10.8.0.33     | 10.8.0.38     | 10.8.0.39 |      8       |        6         |
|   6   | 10.8.0.40 | 255.255.255.248 | 10.8.0.41     | 10.8.0.46     | 10.8.0.47 |      8       |        6         |


Configuración de cada uno de los routers: 
## R1
Configurando ip address
``` bash
configure terminal
int f0/0
ip address 10.8.0.1 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.17 255.255.255.248
no shutdown
exit
```
Configurando rip
```bash
configure terminal
router rip
version 2
network 10.8.0.0
network 10.8.0.16
end
```
Configurando GLBP Activo R1
```bash
int f0/0
glbp 1 ip 10.8.0.46
glbp 1 preempt
glbp 1 priority 150
glbp 1 load-balancing round-robin
```
## R2
Configurando ip address
```bash
configure terminal
int f0/0
ip address 10.8.0.9 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.25 255.255.255.248
no shutdown
exit
```
Configurando rip
```bash
configure terminal
router rip
version 2
network 10.8.0.8
network 10.8.0.24
end
```
Configurando GLBP pasivo R2
```bash
int f0/0
glbp 1 ip 10.8.0.46
glbp 1 load-balancing round-robin
```
## R3
Configurando ip address
```bash
configure terminal
int f0/0
ip address 10.8.0.2 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.33 255.255.255.248
no shutdown
exit
```
Configurando rip
```bash
configure terminal
router rip
version 2
network 10.8.0.0
network 10.8.0.32
end
```
Configurando HSRP pasivo R3
```bash
int f0/0
standby 1 ip 10.8.0.46
```
## R4
Configurando ip address
```bash
configure terminal
int f0/0
ip address 10.8.0.10 255.255.255.248
no shutdown
exit
int f2/0
ip address 10.8.0.41 255.255.255.248
no shutdown
exit
```
Configurando rip
```bash
configure terminal
router rip
version 2
network 10.8.0.8
network 10.8.0.40
end
```
Configurando HSRP Activo R4
```bash
int f0/0
standby 1 ip 10.8.0.46
standby 1 priority 150
standby 1 preempt
```

# Topología 2
![](https://github.com/cesarchs/-REDES1-Proyecto2_G8/blob/main/imgs/topo2.jpeg)



# Topología 3
![](https://github.com/cesarchs/-REDES1-Proyecto2_G8/blob/main/imgs/topo3.jpeg)


## Configuración de la VPN
| PASOS| DESCRIPCION| 
|-------------|------------------------|
| 1           | Abrir consola de SSH |
| 2           | Ejecutar comando "sudo apt-get update" |
| 3           | Ejecutar comando "sudo apt-get upgrade"|
| 4           | Ejecutar comando "sudo wgethttps://cubaelectronica.com/OpenVPN/openvpn-install.sh"|
| 5           | Ejecutar comando "sudo bash openvpn -install.sh"|
| 6           | Ingresar la ip interna de la VM |
| 7           | Ingresar la ip externa de la VM |
| 8           | Seleccionar el protocolo (UDP) |
| 9           | Seleccionar el puerto (1194) |
| 10           | Seleccionar la DNS |
| 11           | Crear clientes para cada integrante |
| 12           | Descargar OPENVPN|
| 13           | Ejecutar el archivo .EXE |
| 14           | Aceptar termino y condiciones |
| 15           | Instalar software |
| 16           | Abrir el software|
| 17           | Importar el archivo .OVPN y conectar a la red|