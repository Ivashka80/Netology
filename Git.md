# Домашнее задание к занятию «Git»

### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в GitHub и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw.
   2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите сверху название занятия, ваши фамилию и имя;
      - в каждом задании добавьте решение в требуемом виде — текст, код, скриншоты, ссылка;
      - для корректного добавления скриншотов используйте [инструкцию «Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
      - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
   4. После завершения работы над домашним заданием сделайте коммит `git commit -m "comment"` и отправьте его на GitHub `git push origin`.
   5. Для проверки домашнего задания в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем GitHub.
   6. Любые вопросы по выполнению заданий задавайте в чате учебной группы или в разделе «Вопросы по заданию» в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!

---

### Задание 1

**Что нужно сделать:**

1. Зарегистрируйте аккаунт на [GitHub](https://github.com/).

<details>

![01](https://github.com/Ivashka80/Netology/assets/121082757/8b775232-df62-4189-8658-cd11bc208522)

</details>

2. Создайте публичный репозиторий. Обязательно поставьте галочку в поле «Initialize this repository with a README».

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/376c245b-7253-4b3c-9083-ce58eba365dc)
 
</details>

3. Склонируйте репозиторий, используя https протокол `git clone ...`.

<details>

Клонирование сделано с помощью SSH-ключа
 
![image](https://github.com/Ivashka80/Netology/assets/121082757/b618b981-624f-4eaf-8a25-7bf3d4171fc8)

</details>

4. Перейдите в каталог с клоном репозитория.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/77fe2889-d440-428c-8d7d-3b6fa703867e)

</details>

5. Произведите первоначальную настройку Git, указав своё настоящее имя и email: `git config --global user.name` и `git config --global user.email johndoe@example.com`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/ab309d1d-7d31-4405-b61a-5c9906b62d87)

</details>

6. Выполните команду `git status` и запомните результат.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/1b73580a-634a-4a5a-8808-05cf453a4295)

</details>

7. Отредактируйте файл README.md любым удобным способом, переведя файл в состояние Modified.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/f29c546f-12e0-4c32-ab3a-47854652a5ee)

</details>

8. Ещё раз выполните `git status` и продолжайте проверять вывод этой команды после каждого следующего шага.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/f31d9fed-5050-45cc-8c6a-f7fcdb0ee551)

</details>

9. Посмотрите изменения в файле README.md, выполнив команды `git diff` и `git diff --staged`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/8de874e5-8edf-4a01-8dba-c9cec25a7f02)

</details>

10. Переведите файл в состояние staged или, как говорят, добавьте файл в коммит, командой `git add README.md`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/6d6f3ca5-2548-451e-9bea-8a17e4f966fe)

</details>

11. Ещё раз выполните команды `git diff` и `git diff --staged`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/b7bcdddf-f3b6-49ed-8557-92e103b3ea62)

</details>

12. Теперь можно сделать коммит `git commit -m 'First commit'`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/7f51ae64-b481-4bdc-8b2f-78d872b5c7c3)

</details>

13. Сделайте `git push origin master`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/7ffc81ad-63e4-4af1-ac61-18a6356bbfe7)

![image](https://github.com/Ivashka80/Netology/assets/121082757/0b215459-e81b-4d05-a0ef-bea0f337b4f4)

![image](https://github.com/Ivashka80/Netology/assets/121082757/e1bce582-66ae-434a-92d0-87bee1b365f3)

</details>

В качестве ответа добавьте ссылку на этот коммит в ваш md-файл с решением.

[Ссылка](https://github.com/Ivashka80/my-first-github/commit/5ce0e2f7275f9a42263a9c92cde3f904df31ae27)

---

### Задание 2

**Что нужно сделать:**

1. Создайте файл .gitignore (обратите внимание на точку в начале файла) и проверьте его статус сразу после создания.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/83bd9228-2edb-4625-9718-e14f5ed5ffbc)

</details>

2. Добавьте файл .gitignore в следующий коммит `git add...`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/406041e7-086c-4c81-9feb-9e7f191b4e77)

</details>

3. Напишите правила в этом файле, чтобы игнорировать любые файлы `.pyc`, а также все файлы в директории `cache`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/517da4e6-9a7b-4624-a93d-4ada559e150f)

</details>


4. Сделайте коммит и пуш.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/f9f575fb-5ed8-43a7-9ecd-ac11819f5626)

![image](https://github.com/Ivashka80/Netology/assets/121082757/5cb012d4-1f49-41aa-9af2-7ca8586d3c43)

</details>

В качестве ответа добавьте ссылку на этот коммит в ваш md-файл с решением.

[Ссылка](https://github.com/Ivashka80/my-first-github/commit/6ccf807a31c068e97663a092cd5d2ae1a9223d9d)

---

### Задание 3

**Что нужно сделать:**

1. Создайте новую ветку dev и переключитесь на неё.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/36115cdd-09a7-4793-a375-c94b79a4e016)

</details>

2. Создайте файл test.sh с произвольным содержимым.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/59357a94-a61d-4c50-8114-bf7861aef850)

![image](https://github.com/Ivashka80/Netology/assets/121082757/4ff300ef-81e4-4e4f-8f96-60929639d13b)

</details>

3. Сделайте несколько коммитов и пушей, имитируя активную работу над этим файлом.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/44cbf1ff-34b0-4344-a1a8-402faf0aed94)

![image](https://github.com/Ivashka80/Netology/assets/121082757/89a255ab-27a0-45d0-8048-6555a5ef9b65)

![image](https://github.com/Ivashka80/Netology/assets/121082757/92a7d9a1-8307-40c3-8dc0-402622e18466)

![image](https://github.com/Ivashka80/Netology/assets/121082757/6a72645d-9fdb-4291-8ebb-3259fe66c0ff)

![image](https://github.com/Ivashka80/Netology/assets/121082757/fb481c84-6d01-4e17-a232-9b29f756cf26)

</details>

   4. Сделайте мердж этой ветки в основную. Сначала нужно переключиться на неё, а потом вызывать `git merge`.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/1bde333c-b494-4348-a85e-95f4c1f91bb6)

</details>

5. Сделайте коммит и пуш.

<details>

![image](https://github.com/Ivashka80/Netology/assets/121082757/bd5c6c98-25e3-4f29-9e95-a3615e31e56f)

![image](https://github.com/Ivashka80/Netology/assets/121082757/06f8c461-5a4f-4287-a317-fbf7efa9755b)

![image](https://github.com/Ivashka80/Netology/assets/121082757/dac733c1-1d78-483c-b5db-576b0b32ca0d)

</details>

В качестве ответа прикрепите ссылку на граф коммитов https://github.com/ваш-логин/ваш-репозиторий/network в ваш md-файл с решением.

[Ссылка](https://github.com/Ivashka80/my-first-github/network) на граф.


---
## Дополнительные задания* (со звёздочкой)

Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.

---
### Задание 4*

Сэмулируем конфликт. Перед выполнением изучите с [документацию](https://git-scm.com/book/ru/v2/%D0%98%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-Git-%D0%9F%D1%80%D0%BE%D0%B4%D0%B2%D0%B8%D0%BD%D1%83%D1%82%D0%BE%D0%B5-%D1%81%D0%BB%D0%B8%D1%8F%D0%BD%D0%B8%D0%B5).

**Что нужно сделать:**

1. Создайте ветку conflict и переключитесь на неё.
2. Внесите изменения в файл test.sh. 
3. Сделайте коммит и пуш.
4. Переключитесь на основную ветку.
5. Измените ту же самую строчку в файле test.sh.
6. Сделайте коммит и пуш.
7. Сделайте мердж ветки conflict в основную ветку и решите конфликт так, чтобы в результате в файле оказался код из ветки conflict.

В качестве ответа на задание прикрепите ссылку на граф коммитов https://github.com/ваш-логин/ваш-репозиторий/network в ваш md-файл с решением.
