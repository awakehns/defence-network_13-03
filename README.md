# Домашнее задание к занятию "`Защита сети`" - `Демин Герман`

### Подготовка

Установка Suricata и Fail2Ban:

```
sudo dnf install suricata fail2ban -y

sudo dnf install virtualbox
```

Kali уже установлена в virtualbox

Установлены Suricata и Fail2Ban:
![install-suricata-fail2ban](/img/install-suricata-fail2ban)

### Заданине 1

Разведка системы через nmap с Kali:

```
sudo nmap -sA 192.168.1.13

sudo nmap -sT 192.168.1.13

sudo nmap -sS 192.168.1.13

sudo nmap -sV 192.168.1.13
```

Запуск команд nmap с Kali:
![nmap](/img/nmap.png)

### Заданине 2

Включение ssh защиты в fail2ban:

```
sudo nano /etc/fail2ban/jail.con

sudo systemctl restart fail2ban 
```

Конфиг fail2ban со включенной защитой:

![fail2ban-enable-ssh](/img/fail2ban-enable-ssh.png)

Атака хоста с Kali через hydra:

```
nano users.txt

nano pass.txt

hydra -L users.txt -P pass.txt -t 2 -I 192.168.1.13 ssh
```

Блокировка атаки:
![block-kali](/img/block-kali.png)

Логи fail2ban:
![ban](/img/ban.png)

В логи suricata ничего не попало. Кроме того, как видно из команды, мне пришлось добавить ключ -t, ведь иначе атаки гидры блокировались на уровне sshd сервера из-за большого количества запущенный одновременно процессов. Стоит отметить, что если удачный пароль стоит в 1-2 строчке, а логинов не слишком много, из которых также есть удачный, то fail2ban не успевает заблокировать kali и происходит успешная атака.

Успешная атака:
![access](/img/access.png)
