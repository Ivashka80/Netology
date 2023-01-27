### Задание 1.


Дан скрипт:
<details>
  

```bash
#!/bin/bash
PREFIX="${1:-NOT_SET}"
INTERFACE="$2"

[[ "$PREFIX" = "NOT_SET" ]] && { echo "\$PREFIX must be passed as first positional argument"; exit 1; }
if [[ -z "$INTERFACE" ]]; then
    echo "\$INTERFACE must be passed as second positional argument"
    exit 1
fi

for SUBNET in {1..255}
do
	for HOST in {1..255}
	do
		echo "[*] IP : ${PREFIX}.${SUBNET}.${HOST}"
		arping -c 3 -i "$INTERFACE" "${PREFIX}.${SUBNET}.${HOST}" 2> /dev/null
	done
done
```
</details>

Измените скрипт так, чтобы:

- для ввода пользователем были доступны все параметры. Помимо существующих PREFIX и INTERFACE, сделайте возможность задавать пользователю SUBNET и HOST;
- скрипт должен работать корректно в случае передачи туда только PREFIX и INTERFACE
- скрипт должен сканировать только одну подсеть, если переданы параметры PREFIX, INTERFACE и SUBNET
- скрипт должен сканировать только один IP-адрес, если переданы PREFIX, INTERFACE, SUBNET и HOST
- не забывайте проверять вводимые пользователем параметры с помощью регулярных выражений и знака `~=` в условных операторах 
- проверьте, что скрипт запускается с повышенными привилегиями и сообщите пользователю, если скрипт запускается без них


### Ответ

К сожалению, я не смог выполнить данное задание. Как я понимаю, надо ввести агрументы для ```SUBNET``` и ```HOST```. Но как заставить их работать, я не могу сообразить.
Прошу изучить мой скрипт. У меня выводит при отладке такую ошибку:
![Screen Shot 2023-01-27 at 12 55 08](https://user-images.githubusercontent.com/121082757/215058150-bc588381-f905-4a99-a5b0-db0e4258d938.png)



```bash
#!/bin/bash
INTERFACE=$1
PREFIX=$2
SUBNET=$3
HOST=$4

trap 'echo "Ping exit (Ctrl-C)"; exit 1' 2

    if [[ -z $INTERFACE ]]; then
        echo "$\INTERFACE must be passed as first positional argument"; exit 1
    elif [[ -z $PREFIX ]]; then
    echo "$\PREFIX must be passed as second positional argument"; exit 1
    fi

        if [[ -z $SUBNET ]]; then
           for SUBNET in {0..255}
           do
                if  [[ -z $HOST ]]; then
                   for HOST in {0..255}
                   do

        echo "IP : $PREFIX.$SUBNET.$HOST"
        arping -c 3 -i $INTERFACE $PREFIX"."$SUBNET"."$HOST  2> /dev/null
        done
        fi

```