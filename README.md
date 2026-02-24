# Домашнее задание к занятию «Защита сети» - `Яковлева Александра`

Подготовка к выполнению заданий
Подготовка защищаемой системы:
установите Suricata,
установите Fail2Ban.
Подготовка системы злоумышленника: установите nmap и thc-hydra либо скачайте и установите Kali linux.
Обе системы должны находится в одной подсети.

# Задание 1
Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

sudo nmap -sA 
<img width="1830" height="722" alt="sA" src="https://github.com/user-attachments/assets/b8953a88-31b3-486a-9426-852e0a08ead2" />

sudo nmap -sT 
<img width="1919" height="626" alt="sT" src="https://github.com/user-attachments/assets/36d566b2-5c1a-4f5b-a0e8-0e1fae5fa182" />

sudo nmap -sS 
<img width="1853" height="467" alt="sS" src="https://github.com/user-attachments/assets/54baa82d-3094-475b-8392-115fb43cfb71" />

sudo nmap -sV 
<img width="1875" height="556" alt="sV" src="https://github.com/user-attachments/assets/f1542cdf-54a0-4c88-babf-9e2cf57bc611" />

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.

Suricata сработал везде, кроме первого запроса -sA. В остальных же случаях лог Suricata выдает, что происходило подозрительное скарирование и классификация идет как "Потенциально опасный трафик" и "Возможна утечка информации".

Fail2Ban во всех случаях молчал.

# Задание 2
Проведите атаку на подбор пароля для службы SSH:

hydra -L users.txt -P pass.txt < ip-адрес > ssh

Настройка hydra:
создайте два файла: users.txt и pass.txt;
в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.
Дополнительная информация по hydra: https://kali.tools/?p=1847.

Включение защиты SSH для Fail2Ban:
открыть файл /etc/fail2ban/jail.conf,
найти секцию ssh,
установить enabled в true.
Дополнительная информация по Fail2Ban:https://putty.org.ru/articles/fail2ban-ssh.html.

В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.

с выключенной службой
Пароль подобран. В логе файла auth видна операция подбора пароля. Suricata также показывает сканирование ssh. Лог-файл Fail2ban ничего не показал.
<img width="1919" height="1079" alt="jailOFFfauthLog" src="https://github.com/user-attachments/assets/f8c7533c-4afe-4ee8-9be8-5db888ab9575" />
<img width="1905" height="1030" alt="jailOFFsuricataLOG" src="https://github.com/user-attachments/assets/ea3ea8c7-bb64-4f00-a121-efe7063cbcba" />

с включенной логи были только в file2ban
Попытка подключения не удалась. Лог-файл Fail2ban также показывает попытку подключения. 
<img width="872" height="719" alt="jailONlog" src="https://github.com/user-attachments/assets/937e21f9-cb40-4dec-8075-e58727063565" />

