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

reg_PREFIX='^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})\.)(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1,2})'
reg_SUBNET='^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1})'
reg_HOST='^(25[0-5]|2[0-4][0-9]|1[0-9]{2}|[0-9]{1})'

if [[ -z $INTERFACE ]]; then
   echo "\$INTERFACE должен быть указан первым аргументом"
fi

if [[ -z $PREFIX ]]; then
   echo "\$PREFIX должен быть указан вторым аргументом в виде числе через точку (например, 100.100)";  exit 2
elif [[ $PREFIX =~ $reg_PREFIX ]]; then
    echo "\$PREFIX должен быть указан аргументом в виде числе через точку (например, 100.100)"; exit 2
fi

if [[ $SUBNET =~ $reg_SUBNET ]]; then
        echo "\$SUBNET должен быть числом от 0 до 255"; exit 2
elif [[ -z $SUBNET ]]; then
      SUBNET=`seq 0 255`
fi

if [[ $HOST =~ $reg_HOST ]]; then
        echo "\$HOST должен быть числом от 0 до 255"; exit 2
elif [[ -z $HOST ]]; then
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
