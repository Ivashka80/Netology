## Задание 1.
- Создайте пользователя student1 с оболочкой bash, входящего в группу student1.
- Создайте пользователя student2, входящего в группу student2.
- Приведите ответ в виде снимков экрана.

#### Ответ
Cоздаем группу - `sudo groupadd student1`

Проверим

![Снимок01](https://user-images.githubusercontent.com/121082757/208647821-753aae70-96c7-4a5c-acec-7f3868241281.JPG)

Теперь создаем пользователя, чтобы он входил в ранее созданную группу - `sudo useradd -g student1 -s /bin/bash student1`

![Снимок02](https://user-images.githubusercontent.com/121082757/208647881-bce44244-ef74-440c-9ff0-5df0cebe8e60.JPG)

Для пользователя student2 делаем то же самое.

![Снимок03](https://user-images.githubusercontent.com/121082757/208648229-978ea002-909a-4c85-bd0d-f03aa9cdec9f.JPG)


