University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)

Year: 2022/2023

Group: K33212

Author: Sobolevskaya Nadezhda Sergeevna

Lab: Lab2

Date of create: xx.xx.2022

Date of finished: xx.xx.2022

# Отчет по лабораторной работе №1: "Установка ContainerLab и развертывание тестовой сети связи"

## Цель работы

Ознакомиться с инструментом ContainerLab и методами работы с ним, изучить работу VLAN, IP адресации и т.д.

## Схема сети


## Ход работы
#### 1. Содержимое файла lab02.clab.yaml для развертывания виртуальной сети:
```
name: lab2

mgmt:
  network: staticNet
  ipv4_subnet: 172.20.10.0/24

topology:
  nodes:
    R01.MSK:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 172.20.10.2
    
    R01.FRT:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 172.20.10.3

    R01.BRL:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 172.20.10.4

    PC1: 
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 172.20.10.15

    PC2: 
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 172.20.10.16

    PC3: 
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 172.20.10.17

  links:
    - endpoints: ["R01.MSK:eth2", "R01.BRL:eth2"]
    - endpoints: ["R01.BRL:eth3", "R01.FRT:eth2"]
    - endpoints: ["R01.MSK:eth3", "R01.FRT:eth3"]
    - endpoints: ["R01.MSK:eth4", "PC1:eth2"]
    - endpoints: ["R01.FRT:eth4", "PC2:eth2"]
    - endpoints: ["R01.BRL:eth4", "PC3:eth2"]
```

#### 2. Настройка сетевых устройств. Export конфигураций.

- Роутер R01.MSK (172.20.10.2): 

![image](https://user-images.githubusercontent.com/43678322/207968819-a75b02c2-fbbb-49ae-8d7a-6385b4310dfc.png)

- Роутер R01.FRT (172.20.10.3): 

![image](https://user-images.githubusercontent.com/43678322/207968869-c8c34bc3-851c-4099-bb37-e6e33f100e18.png)

- Роутер R01.BRL (172.20.10.4): 

![image](https://user-images.githubusercontent.com/43678322/207968982-d1f4bd44-0e12-4c4b-bff8-c0873b63f440.png)

- ПК PC1 (172.20.10.15): 

![image](https://user-images.githubusercontent.com/43678322/207969128-1e765f15-27bd-440c-adde-63e0377cca7c.png)

- ПК PC2 (172.20.10.16): 

![image](https://user-images.githubusercontent.com/43678322/207969213-d42b855a-415c-4a01-abe9-160591bfdcd1.png)

- ПК PC3 (172.20.10.17): 

![image](https://user-images.githubusercontent.com/43678322/207969307-c5ca736a-1872-4a82-a467-0edfaec0db79.png)

#### 3. Ping адресов устройств:

![image](https://user-images.githubusercontent.com/43678322/207968441-45c3c233-4d45-4638-bf95-df2a1669a05b.png)
![image](https://user-images.githubusercontent.com/43678322/207968480-b08debfc-692f-46f7-a7b1-1b0cf564885f.png)
![image](https://user-images.githubusercontent.com/43678322/207968408-2e9c6abf-b133-400a-83ea-032a66dd8d2d.png)

#### 4. Вывод
