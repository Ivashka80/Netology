# Домашнее задание к занятию «Terraform»


### Оформление домашнего задания

1. Домашнее задание выполните в [Google Docs](https://docs.google.com/) и отправьте на проверку ссылку на ваш документ в личном кабинете.  
1. В названии файла укажите номер лекции и фамилию студента. Пример названия: 7.2. Terraform — Александр Александров.
1. Перед отправкой проверьте, что доступ для просмотра открыт всем, у кого есть ссылка. Если нужно прикрепить дополнительные ссылки, добавьте их в свой Google Docs.

Любые вопросы по решению задач задавайте в чате учебной группы.

---

### Задание 1

**Ответьте на вопрос в свободной форме.**

Опишите виды подхода к IaC:

 * функциональный;
 * процедурный;
 * интеллектуальный.

### Ответ

 * функциональный подход определяет желаемое состояние системы и то, какие ресурсы  нужны и какими свойствами они должны обладать и инструмент IaC поможет настроить его. Этот подход также сохраняет список текущего состояния системных объектов, что упрощает управление инфраструктурой.
 * процедурный подход определяет конкретные команды, необходимые для достижения желаемой конфигурации. Далее эти команды должны быть выполнены в правильном порядке.
 * интеллектуальный подход считается самым сложным в описании, так как он указывает порядок конфигурирования инфраструктуры. Для использования готовых конфигураций IaC предусматривает методики push и pull. Разница между ними — в инициаторе изменений конфигураций целевого хоста. В режиме pull инициатором получения своей конфигурации выступает сам хост. В push режиме он получает конфигурацию с управляющего сервера.

---

### Задание 2

**Ответьте на вопрос в свободной форме.**

Как вы считаете, в чём преимущество применения Terraform?

### Ответ

Terraform — это программный инструмент для управления инфраструктурой от компании Hashicorp. С помощью него можно развертывать инфраструктуру и управлять ею на различных облачных платформах. Основное преимущество Terraform заключается в том, что он позволяет автоматизировать процесс создания и управления инфраструктурой. Это делает его очень полезным инструментом для DevOps-инженеров и системных администраторов. 
Terraform используется для автоматизации развертывания и управления инфраструктурой в облачных средах. Он позволяет управлять различными типами ресурсов, такими как виртуальные машины, сети, хранилища данных и другие, с помощью одного инструмента.

---

### Задание 3

**Ответьте на вопрос в свободной форме.**

Какие минусы можно выделить при использовании IaC?

### Ответ

Среди недостатков IaC выделяют:
* Значительное время и усилия, которые нужно потратить на настройку и тестирование инфраструктуры в начале проекта.
* Необходимость наличия знаний в области программирования и DevOps.
* Может потребовать значительных инвестиций в инфраструктуру и инструменты.

Кроме того, IaC нуждается в дополнительных инструментах, таких как система управления конфигурацией и автоматизацией, в результате чего в системе могут возникать ошибки. Любые ошибки могут быстро распространяться по серверам, особенно там, где есть обширная автоматизация, поэтому очень важно контролировать версии и осуществлять всестороннее предварительное тестирование.

Если администраторы изменяют конфигурации сервера за пределами установленного шаблона, возникает вероятность отклонения конфигурации без использования дополнительных инструментов управления изменениями. 

Если устаревшие инструменты безопасности и мониторинга не подходят для обработки IaC, потребуются дополнительные инструменты с дополнительным тестированием для их интеграции в рабочие процессы.

Еще одна проблема с IaC заключается в том, что она возлагает на разработчиков больше ответственности за понимание того, как писать эффективный код, который легко транслируется в производственные среды.

---

### Задание 4

**Выполните действия и приложите скриншоты запуска команд.**

Установите Terraform на компьютерную систему (виртуальную или хостовую), используя лекцию или [инструкцию](https://learn.hashicorp.com/tutorials/terraform/install-cli).    

В связи с недоступностью ресурсов для загрузки Terraform на территории РФ, вы можете  воспользоваться VPN или использовать зеркало YandexCloud.   
- [Документация по провайдерам Terraform в зеркале YandexCloud](https://registry.tfpla.net/browse/providers)   
- [Зеркало YandexCloud для загрузки Terraform](https://hashicorp-releases.yandexcloud.net/terraform/)    
- [Инструкция по настройке провайдера](https://cloud.yandex.ru/docs/tutorials/infrastructure-management/terraform-quickstart#configure-terraform)  


### Ответ

---

## Дополнительные задания* (со звёздочкой)

Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.лнить, если хотите глубже и/или шире разобраться в материале.

---

### Задание 5*

**Ответьте на вопрос в свободной форме.**

Перечислите основные функции, которые могут использоваться в Terraform. 
