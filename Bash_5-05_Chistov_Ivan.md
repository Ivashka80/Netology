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


Скрипт
<details>

```bash
#!/bin/bash

INTERFACE=$1
PREFIX=$2
SUBNET=$3
HOST=$4

username=`id -nu`
if [ "$username" != "root" ]
then
        echo "Must be root to run \"`basename $0`\"."
        exit 1
fi

trap 'echo "Ping exit (Ctrl-C)"; exit 1' 2

if [[ -z "$INTERFACE" ]]; then
    echo "\$INTERFACE must be passed as first positional argument"
fi

[[ -z "$PREFIX" ]] && { echo "\$PREFIX must be passed as second positional argument"; exit 1; }

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
                arping -c 1 -i $INTERFACE $PREFIX.$SUBNET.$HOST 2> /dev/null
        done
done

```
</details>

Скрипт запускается от пользователя root. В противном случае будет сообщение об ошибке.    

![001](https://user-images.githubusercontent.com/121082757/215254173-9431b9dd-743f-4f7a-ad0b-942e6314830d.JPG)

Запуск скрипта выполняется с обязательным указанием сначала INTERFAS, затем EPREFIX. Если не указать, будет выдано соответствующее сообщение:

![image](https://user-images.githubusercontent.com/121082757/217589861-f6eed979-dc0d-49c3-ab4d-6bc7d7e2a1cd.png)

- Запуск скрипта только с INTERFACE и PREFIX.
<details>

![image](https://user-images.githubusercontent.com/121082757/217590356-4938d755-f991-4ced-875b-b755b09c2b74.png)
	
</details>

- Запуск скрипта с добавлением SUBNET
<details>

![image](https://user-images.githubusercontent.com/121082757/217590519-42dcce40-9326-4410-ae08-030b2c50aa64.png)

</details>

- Запуск скрипта с добавление HOST. В этом случае сканируется только указанный IP-адрес.
<details>

![image](https://user-images.githubusercontent.com/121082757/217590642-ad309a27-4c4c-40d0-888a-6673ec95d652.png)

</details>
