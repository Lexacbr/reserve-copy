# Домашнее задание к занятию  «Резервное копирование»

------

### Задание 1
- Составьте команду rsync, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию `/tmp/backup`
- Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)
- Необходимо сделать так, чтобы rsync подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.
- На проверку направить скриншот с командой и результатом ее выполнения

---
### Ответ на задание 1

---
- Что я делал:
* Запустил команду из домашней дироктории:
``` bash
rsync -ac --delete --exclude=".*/" . /tmp/backup
```
![scrsh](https://github.com/Lexacbr/reserve-copy/blob/main/scrsh/lsla.png)

![scrsh](https://github.com/Lexacbr/reserve-copy/blob/main/scrsh/abc.png)

------

### Задание 2
- Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.
- Резервная копия должна быть полностью зеркальной
- Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции
- Резервная копия размещается локально, в директории `/tmp/backup`
- На проверку направить файл crontab и скриншот с результатом работы утилиты.

------
* Что я делеал:
---
* Создал файл скрипта backub.sh следующего содержания:
```bash
#! /bin/bash
rsync -a --delete /home/abc/ /tmp/backup
if [ "$?" -eq 0 ]; then
        logger "Rsync make a successful backup"
else    logger "Rsync backup error"
fi
```
---
* Делаю скрипт исполняемым:
```bash
sudo chmod +x backup.sh 
```
---
* Добавляю в планировщик. Вызываю планировщик командой:
```bash
sudo crontab -e
```
---
* Делаю запись: запускать срипт /home/abc/backup.sh в 0-ю минуту в 7 часов утра каждый день:

```bash
0 7 * * * /home/vboxuser/backup.sh
```
---
![scrsh](https://github.com/Lexacbr/reserve-copy/blob/main/scrsh/cron.png)

------

