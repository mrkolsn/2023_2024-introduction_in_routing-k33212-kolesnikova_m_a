University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)  
Year: 2023/2024  
Group: K33212  
Author: Kolesnikova Maria Alekseevna  
Lab: Lab1  
Date of create: 12.10.2023  
Date of finished: 31.10.2023  

## Лабораторная работ №1 "Установка ContainerLab и развертывание тестовой сети связи"    

## <a>Ход работы</a>   
#### <a>Подготовка</a>   
1. Установка Docker на рабочий компьютер
2. Установка make и клонирование репозитория hellt/vrnetlab
3. Сборка образа с помощью ```make docker-image``` 
4. Установка ContainerLab с использованием специального скрипта из официального репозитория:
   ```bash -c "$(curl -sL https://get.containerlab.dev)"```

#### <a>Построение трехуровневой сети связи классического предприятия</a>  
1. Содержимое yaml файла, который использовался для развертывания тестовой сети
    ```
    name: lab1
    mgmt:
      network: static
      ipv4-subnet: 192.168.48.0/24
    topology:
      nodes:
        R01:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 192.168.48.2
    
        Linux1:
          kind: linux
          image: alpine:latest
          mgmt-ipv4: 192.168.48.3
    
        Linux2:
          kind: linux
          image: alpine:latest
          mgmt-ipv4: 192.168.48.4
          
        SW01.L3.01:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 192.168.48.5
    
        SW02.L3.01:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 192.168.48.6
    
        SW02.L3.02:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 192.168.48.7
    
      links:
          - endpoints: ["R01:eth1", "SW01.L3.01:eth1"]
          - endpoints: ["SW01.L3.01:eth2", "SW02.L3.01:eth1"]
          - endpoints: ["SW02.L3.01:eth2", "Linux1:eth1"]
          - endpoints: ["SW01.L3.01:eth3", "SW02.L3.02:eth1"]
          - endpoints: ["SW02.L3.02:eth2", "Linux2:eth1"]
    ```
3. Сборка:  
   ```sudo containerlab deploy lab1.yaml```
4. Построение схемы сети:  
   ```sudo containerlab graph```  
   ![photo_2023-10-30_00-44-58](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/dab5bde2-f325-4e0f-8a66-a23b7e035cf4)
   
#### <a>5. Настройка R01</a>  
  ![photo_5_2023-10-30_00-42-32](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/815c22db-a47f-440e-903c-77b706a53352)

#### <a>6. Настройка SW01.L3.01</a>    
  ![photo_6_2023-10-30_00-42-32](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/490f01a3-49f6-4692-841a-e2bfa30c3ecd)

#### <a>7. Настройка SW02.L3.01</a>    
  ![photo_4_2023-10-30_00-42-32](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/328e6ec5-7f97-4116-a646-9879e8103db7)

#### <a>8. Настройка SW02.L3.02</a>    
  ![photo_3_2023-10-30_00-42-32](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/b75f8b02-ed5f-40ed-b660-2fa83050a202)

#### <a>9. Результаты пингов:</a> 
  ![photo_2_2023-10-30_00-42-32](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/4f7cdbf1-37d0-46f8-8b5c-1ccaf408f4ad)
  ![photo_1_2023-10-30_00-42-32](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/6e1f5e67-b16c-4d1c-aef8-181a00ebec9e)
