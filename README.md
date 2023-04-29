Васёв А.В.

# Keepalived/vrrp

## Задание 1

### Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived.
### В качестве решения предоставьте:
### - рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;
### - скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.

```
vrrp_instance netology {
state MASTER
interface enp0s8
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.0.1
}
virtual_ipaddress {
192.168.0.100 dev enp0s8 label enp0s8:vip
}
}
```

```
vrrp_instance netology {
state BACKUP
interface enp0s8
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.0.2
}
virtual_ipaddress {
192.168.0.100 dev enp0s8 label enp0s8:vip
}
}
```


![alt text](https://github.com/rus42/keepalived/blob/main/Task_1.png)

## Задание 2

### Проведите тестирование работы ноды, когда один из интерфейсов выключен. Для этого:
### добавьте ещё одну виртуальную машину и включите её в сеть;
### на машине установите Wireshark и запустите процесс прослеживания интерфейса;
### запустите процесс ping на виртуальный хост;
### выключите интерфейс на одной ноде (мастер), остановите Wireshark;
### найдите пакеты ICMP, в которых будет отображён процесс изменения MAC-адреса одной ноды на другой.

![alt text](https://github.com/rus42/keepalived/blob/main/Task_2.1.png)
![alt text](https://github.com/rus42/keepalived/blob/main/Task_2.2.png)


