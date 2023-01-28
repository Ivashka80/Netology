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

У меня получилось так, что SUBNET и HOST надо задавать после ввода PREFIX и INTERFACE. 

Скрипт
<details>

```bash
#!/bin/bash

PREFIX=$1
INTERFACE=$2
SUBNET=$3
HOST=$4

username=`id -nu`
if [ "$username" != "root" ]
then
        echo "Must be root to run \"`basename $0`\"."
        exit 1
fi

trap 'echo "Ping exit (Ctrl-C)"; exit 1' 2

[[ "$PREFIX" = "NOT_SET" ]] && { echo "\$PREFIX must be passed as first positional argument"; exit 1; }

if [[ -z "$INTERFACE" ]]; then
    echo "\$INTERFACE must be passed as second positional argument"
    exit 1
fi

if [[ -z "$SUBNET" ]]; then
    SUBNET=`seq 0 255`
fi

if [[ -z "$HOST" ]]; then
   HOST=`seq 0 255`
fi

for SUBNET in $SUBNET
do
        for HOST in $HOST
        do
                echo "[*] IP : $PREFIX.$SUBNET.$HOST"
                arping -c 2 -i $INTERFACE $PREFIX.$SUBNET.$HOST 2> /dev/null
        done
done

```
</details>

Скрипт запускается от пользователя root. В противном случае будет сообщение об ошибке.    

![001](https://user-images.githubusercontent.com/121082757/215254173-9431b9dd-743f-4f7a-ad0b-942e6314830d.JPG)

Запуск скрипта выполняется с обязательным указанием PREFIX и INTERFASE. Если не указать, будет выдано соответствующее сообщение, например "PREFIX must be passed as first positional argument".  

- Запуск скрипта только с PREFIX и INTERFACE.
<details>
![002](https://user-images.githubusercontent.com/121082757/215254340-df4c2981-a787-433e-8342-cd4b4bdcbec8.JPG)
</details>

- Запуск скрипта с добавлением SUBNET
</details>
![003](https://user-images.githubusercontent.com/121082757/215254384-4c2ab002-6080-4abd-94e1-b91120364e04.JPG)
<details>

- Запуск скрипта с добавление HOST. В этом случае сканируется только указанный IP-адрес.
</details>
![004](https://user-images.githubusercontent.com/121082757/215254428-d5eb8349-9677-4dae-9ee3-2968e2576025.JPG)
<details>
