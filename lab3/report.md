University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)  
Year: 2023/2024  
Group: K33212  
Author: Kolesnikova Maria Alekseevna  
Lab: Lab3  
Date of create: 02.12.2023  
Date of finished: 12.12.2023  

## Лабораторная работ №3 "Эмуляция распределенной корпоративной сети связи, настройка OSPF и MPLS, организация первого EoMPLS"    

## <a>Ход работы</a>   

#### <a>Построение сети связи</a>  
1. Содержимое yaml файла, который использовался для развертывания тестовой сети
    ```
    name: lab3

    mgmt:
      network: statics
      ipv4-subnet: 172.30.20.0/24

    topology:
      nodes:
        R01_NYC:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.10
    
        R01_LND:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.11
               
        R01_HKI:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.12
             
        R01_SPB:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.13
               
        R01_MSK:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.14
                
        R01_LBN:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.15
              
        PC1:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.16
    
        SGI_Prism:
          kind: vr-ros
          image: vrnetlab/vr-routeros:6.47.9
          mgmt-ipv4: 172.30.20.17
  
      links:
        - endpoints: ["SGI_Prism:eth1","R01_NYC:eth1"]
        - endpoints: ["R01_NYC:eth2","R01_LND:eth1"]
        - endpoints: ["R01_NYC:eth3","R01_LBN:eth1"]
        - endpoints: ["R01_LND:eth2","R01_HKI:eth1"]
        - endpoints: ["R01_LBN:eth2","R01_HKI:eth2"]
        - endpoints: ["R01_LBN:eth3","R01_MSK:eth1"]
        - endpoints: ["R01_HKI:eth3","R01_SPB:eth1"]
        - endpoints: ["R01_SPB:eth2","R01_MSK:eth2"]
        - endpoints: ["R01_SPB:eth3","PC1:eth1"]
    ```
2. Сборка:  
   ```sudo containerlab deploy lab3.yaml```  
   ![deploy](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/755ad3d2-55ca-4f99-bf78-9afb07bc2263)

3. Построение схемы сети:  
   ```sudo containerlab graph```  
   ![graph](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/edadb126-3d48-48eb-a7d6-15ef0711bbbf)

### <a>Текст конфигураций для каждого сетевого устройства</a>
#### <a>4. Настройка R01_SPB с компьютером инженеров в Санк-Петербурге:</a>    
##### <a>Настройка PC1:</a>     
![pc1](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/54bd48d4-658f-4345-b53a-27537a2d9760)
![pc1 2](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/dc0ffb9f-bb9b-4dff-bbc9-d3df981a76c2)

##### <a>5. Настройка R01_SPB:</a>      
![spb](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/5a5b9c63-ad5c-4ce9-bd31-99df9313dbba)


#### <a>Настройка роутеров, которые не связаны с конечными точками и не являются PE(R01_HKI, R01_LBN, R01_LND, R01_MSK):</a>    
##### <a>6. Настройка R01_HKI:</a>  
![hki](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/361e3b60-6a57-44ec-8839-eabfabf7629d)


##### <a>7. Настройка R01_LBN:</a>  
![lbn](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/0983b818-98fa-469f-8459-136d3646d586)

##### <a>8. Настройка R01_LND:</a>  
![lnd](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/eb816bb2-8296-4877-a9c7-3c5dfcf39aa7)


##### <a>9. Настройка R01_MSK:</a>  
![msk](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/b1754a92-3e39-431d-8e37-5c129c0e478a)

#### <a>10. Настройка R01_NYC с сервисом SGI_Prism:</a> 
##### <a>Настройка R01_NYC:</a> 
![nyc](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/78094ff1-bed6-4972-a5fa-b0f14074b577)


##### <a>11. Настройка SGI_Prism:</a>
![sgi_prism](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/bced4cdd-fc7c-445c-8c8f-54e854a64e25)


## <a>12. Результаты пингов и проверка локальной связности:</a>     
#### <a>Прослеживание маршрута следования данных от R01_NYC до R01_SPB</a>:
![маршрут от nyc до spb](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/53419210-efdc-4ccc-94a4-cd8c54571268)

#### <a>Конфигурация MPLS:</a>    
![mpls](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/5448391f-7bb0-4f68-8f18-8705f71dd365)

#### <a>ICMP запрос от SGI_Prism к PC1:</a>    
![icmp запросы от sgi_prism до pc1](https://github.com/mrkolsn/2023_2024-introduction_in_routing-k33212-kolesnikova_m_a/assets/90474013/2d3a6599-fefe-4778-8c0d-a7350f2f9025)

## <a>Выводы</a>  
В результате выполнения данной лабораторной работы были изучены протоколы OSPF и MPLS, механизмы организации EoMPLS.в.
