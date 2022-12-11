University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)

Year: 2022/2023

Group: K33212

Author: Sobolevskaya Nadezhda Sergeevna

Lab: Lab1

Date of create: 18.09.2022

Date of finished: 11.12.2022


# Отчет по лабораторной работе №1: "Установка ContainerLab и развертывание тестовой сети связи"

## Цель работы

Ознакомиться с инструментом ContainerLab и методами работы с ним, изучить работу VLAN, IP адресации и т.д.

## Ход работы
#### 1. Содержимое файла lab1.clab.yaml для развертывания виртуальной сети:
```
name: lab1

mgmt:
  network: statics
  ipv4_subnet: 192.11.11.0/24

topology:
  nodes:
    R01.TEST:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 192.11.11.2

    SW01.01.TEST:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 192.11.11.3

    SW02.01.TEST:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 192.11.11.4

    SW02.02.TEST:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt_ipv4: 192.11.11.5

    PC1:
      kind: linux
      image: ubuntu:latest
      mgmt_ipv4: 192.11.11.6

    PC2:
      kind: linux
      image: ubuntu:latest
      mgmt_ipv4: 192.11.11.7

  links: 
    - endpoints: ["R01.TEST:eth1", "SW01.01.TEST:eth1"]
    - endpoints: ["SW01.01.TEST:eth2", "SW02.01.TEST:eth1"]
    - endpoints: ["SW01.01.TEST:eth3", "SW02.02.TEST:eth1"]
    - endpoints: ["SW02.01.TEST:eth2", "PC1:eth1"]
    - endpoints: ["SW02.02.TEST:eth2", "PC2:eth1"]  

```
#### 2. Схема сети:
<img src='ContainerLab.png' alt="">

#### 3. Разворачивание сети
![image](https://user-images.githubusercontent.com/43678322/206920601-c093a9cb-ff33-43ef-a576-b97bcba3a894.png)
Видим список устройств и их адреса для подключения по ssh admin@192...

#### 4. Export конфигураций сетевых устройств:

- R01.TEST 
![image](https://user-images.githubusercontent.com/43678322/206920272-abf7e411-599f-471e-9828-ee5a626d2d97.png)
- SW01.01.TEST
![image](https://user-images.githubusercontent.com/43678322/206920287-c40a9940-1552-4e6f-8ca2-5d67bea335d4.png)
- SW02.01.TEST
![image](https://user-images.githubusercontent.com/43678322/206920299-1c4e7ed3-4a82-44a5-8f63-333a3742aeb3.png)
- SW02.02.TEST
![image](https://user-images.githubusercontent.com/43678322/206920329-c4a208d3-5e23-4212-b4ce-e8272a739e79.png)

#### 5. Ping адресов устройств:
![image](https://user-images.githubusercontent.com/43678322/206920376-9921e460-808a-44dd-a2eb-4267acd5cb04.png)
![image](https://user-images.githubusercontent.com/43678322/206920386-3c47296f-d02b-4260-98b4-ffc50d6610fb.png)
![image](https://user-images.githubusercontent.com/43678322/206920392-ebba4cc1-37cf-4384-baa8-2f21b535b93a.png)

#### 6. Вывод
В ходе данной лабораторной работы были освоены методы работы с ContainerLab, была изучена работа VLAN, IP адресация и т.д.
