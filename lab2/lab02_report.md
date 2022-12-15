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

![image](https://user-images.githubusercontent.com/43678322/207956838-8ad9778a-40b1-49a7-aae4-fd97970ca343.png)

- Роутер R01.FRT (172.20.10.3): 

![image](https://user-images.githubusercontent.com/43678322/207956993-4a55b902-b835-456e-8e6b-8cc3e7de3ad5.png)

- Роутер R01.BRL (172.20.10.4): 

![image](https://user-images.githubusercontent.com/43678322/207957121-64502b7a-09b9-4c2b-b296-af3fcd06aced.png)


- ПК PC1 (172.20.10.15): 

![image](https://user-images.githubusercontent.com/43678322/207957312-76fee576-2612-4d8b-9422-b9a61b90cb29.png)

- ПК PC2 (172.20.10.16): 

![image](https://user-images.githubusercontent.com/43678322/207957348-77b39e06-bd6b-488e-bf28-449f4f92f702.png)

- ПК PC3 (172.20.10.17): 

![image](https://user-images.githubusercontent.com/43678322/207957392-e7669818-8ad7-4a9c-8f61-177ed291b5ee.png)

#### 3. Ping адресов устройств:

![image](https://user-images.githubusercontent.com/43678322/207968441-45c3c233-4d45-4638-bf95-df2a1669a05b.png)
![image](https://user-images.githubusercontent.com/43678322/207968480-b08debfc-692f-46f7-a7b1-1b0cf564885f.png)
![image](https://user-images.githubusercontent.com/43678322/207968408-2e9c6abf-b133-400a-83ea-032a66dd8d2d.png)

#### 4. Вывод
