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



Скрипт запускается от пользователя root. В противном случае будет сообщение об ошибке.    

![image](https://user-images.githubusercontent.com/121082757/218016750-705d1c58-2945-4d47-8226-db0c99c025d3.png)

Запуск скрипта выполняется с обязательным указанием сначала INTERFASE, затем PREFIX. Если не указать, будет выдано соответствующее сообщение:

![image](https://user-images.githubusercontent.com/121082757/218016624-39168ab1-38ab-4869-8bdc-8bfb1b8023d8.png)

Также происходит проверка вводимых данных для PREFIX. Если неправильно задать, будет сообщение об ошибке

![image](https://user-images.githubusercontent.com/121082757/218015505-5a815821-7015-44e4-aff2-4abe7129e318.png)

Для запуска перебора SUBNET и HOST нужно задать либо точное значение, либо знак вопроса. Если будет задано не число или не будет ввода данных, будет сообщение об ошибке.

![image](https://user-images.githubusercontent.com/121082757/218015928-37f69530-7989-45f3-bab0-6acc8eb4ced1.png)


- Запуск скрипта только с INTERFACE и PREFIX (нажать на "Подробнее").
<details>

![image](https://user-images.githubusercontent.com/121082757/218016208-7eb5eca1-4373-4a66-b4ec-151e4150d90b.png)
	
</details>

- Запуск скрипта с добавлением SUBNET
<details>

![image](https://user-images.githubusercontent.com/121082757/218016298-a40baea7-b453-4dcd-acee-32f26cc0083c.png)

</details>

- Запуск скрипта с добавление HOST. В этом случае сканируется только указанный IP-адрес.
<details>

![image](https://user-images.githubusercontent.com/121082757/218016390-9bb95e36-a5a2-4f1c-8eb9-af2eb0a343e9.png)
  
</details>

Также скрипт позволяет перебирать только SUBNET с заданным HOST

<details>

![image](https://user-images.githubusercontent.com/121082757/218016502-4a267cc7-b7e4-468f-b604-cdc0ec445a27.png)
  
</details>


### СКРИПТ.
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

#Тут пытался регулярки сделать как переменные, но что-то где-то не получается, потому пошел другим путем
#reg_PREFIX="^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})\.(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})"
#reg_SUBNET="^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1})"
#reg_HOST="^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1})"

if [[ -z "$INTERFACE" ]]; then
   echo "\$INTERFACE должен быть указан первым аргументом"
fi

if [[ -z "$PREFIX" ]]; then
   echo "\$PREFIX должен быть указан вторым аргументом в виде числе через точку (например, 100.100)";  exit 1
elif [[ ! "$PREFIX" =~ ^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})\.(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2}) ]]; then
    echo "\$PREFIX должен быть указан аргументом в виде числе через точку (например, 100.100)"; exit 1
fi

# Проверка SUBNET
if [[ -z "$SUBNET" ]]; then
    echo "SUBNET должно быть число от 0 до 255 или знак вопроса (?)"
    exit 1
elif [[ "$SUBNET" == "?" ]]; then
    sSUBNET=$(seq 1 255)
#elif [[ ! $SUBNET =~ ^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1}) ]]; then - неудачный вариант с регуляркой
elif (( SUBNET > 0 && SUBNET < 256 )); then
    sSUBNET=$SUBNET
else
    echo "SUBNET должно быть число от 0 до 255 или знак вопроса (?)"
    exit 1
fi

# Проверка HOST
if [[ -z "$HOST"  ]]; then
    echo "HOST должно быть число от 0 до 255 или знак вопроса (?)"
elif [[ "$HOST" == "?" ]]; then
    sHOST=$(seq 1 255)
#elif [[ ! $HOST =~ ^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1}) ]]; then - неудачный вариант с регуляркой
elif (( HOST > 0 && HOST < 256 )); then
    sHOST=$HOST
else
    echo "HOST должно быть число от 0 до 255 или знак вопроса (?)"
    exit 1
fi

#Запуск ARPING
for SUBNET_ in $sSUBNET; do
    for HOST_ in $sHOST; do
         echo "[*] IP : $PREFIX.$SUBNET_.$HOST_"
         arping -c 2 -i "$INTERFACE" "$PREFIX.$SUBNET_.$HOST_" 2> /dev/null
    done
done

```
</details>
