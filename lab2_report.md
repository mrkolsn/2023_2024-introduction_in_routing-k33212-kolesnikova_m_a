University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)  
Year: 2023/2024  
Group: K33212  
Author: Kolesnikova Maria Alekseevna  
Lab: Lab2  
Date of create: 02.11.2023  
Date of finished: 12.11.2023  

## Лабораторная работ №2 "Эмуляция распределенной корпоративной сети связи, настройка статической маршрутизации между филиалами"    

## <a>Ход работы</a>   

#### <a>Построение сети связи</a>  
1. Содержимое yaml файла, который использовался для развертывания тестовой сети
    ```
    name: lab2
    
    mgmt:
      network: statics
      ipv4-subnet: 172.30.20.0/24
    
    topology:
      nodes:
        R01.MSK:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.13

    R01.BRL:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 172.30.20.14

    R01.FRT:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 172.30.20.15

    PC1:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 172.30.20.16

    PC2:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 172.30.20.17

    PC3:
      kind: vr-ros
      image: vrnetlab/vr-routeros:6.47.9
      mgmt-ipv4: 172.30.20.18

    links:
      - endpoints: ["R01.MSK:eth2", "R01.FRT:eth2"]
      - endpoints: ["R01.MSK:eth1", "R01.BRL:eth1"]
      - endpoints: ["R01.BRL:eth2", "R01.FRT:eth1"]
      - endpoints: ["R01.MSK:eth3", "PC1:eth3"]
      - endpoints: ["R01.FRT:eth3", "PC2:eth3"]
      - endpoints: ["R01.BRL:eth3", "PC3:eth3"]
    ```
2. Сборка:  
   ```sudo containerlab deploy lab2.yaml```  
   ![photo_10_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/1549e914-22b0-465b-92de-b8677f28c040)


4. Построение схемы сети:  
   ```sudo containerlab graph```  
   ![photo_7_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/35c3416f-3636-4418-bd75-c58b71d4ef6f)

   
#### <a>4. Настройка R01.MSK</a>  
  ![photo_9_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/97a2f57c-8f47-4949-8580-6e182d98db3c)


#### <a>4. Настройка R01.FRT</a> 
  ![photo_4_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/c439c86f-ebf1-415e-9715-8e8112597eeb)


#### <a>5. Настройка R01.BRL</a> 
  ![photo_11_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/82968837-9256-4091-9b15-08fe89f7df68)


#### <a>6. Настройка PC1</a>    
  ![photo_2_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/ea81dbd5-c685-419f-8bb5-118c797ed4d6)


#### <a>7. Настройка PC2</a>    
  ![photo_5_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/20a8be4e-a3ef-41fa-b461-a7ac837a4fc6)


#### <a>8. Настройка PC3</a>    
  ![photo_6_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/3a52d73e-2e50-4f88-8f0e-130987108376)


#### <a>9. Результаты пингов:</a> 
  ![photo_3_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/457c227f-2729-44fb-9bd1-822262d8a7c0)
  ![photo_1_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/e3a92c77-58a8-4d32-917e-33ce34da2172)
  ![photo_8_2023-11-12_17-26-30](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/e6b1892d-e52a-4359-84e2-0a1c0c07e251)


