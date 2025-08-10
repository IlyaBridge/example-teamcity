#  «Создание собственных модулей» "`«Teamcity»`" - `Казначеев Илья`
---
https://github.com/LotsmanSM/DevOps-35-Netology/blob/main/devops-05-ci/ci-05-teamcity/README.md

## Подготовка к выполнению
1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа jetbrains/teamcity-server.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа jetbrains/teamcity-agent. Пропишите к нему переменную окружения SERVER_URL: "http://<teamcity_url>:8111".
4. Авторизуйте агент.
5. Сделайте fork репозитория.
6. Создайте VM (2CPU4RAM) и запустите playbook.

---

## Основная часть
1. Создайте новый проект в teamcity на основе fork.
2. Сделайте autodetect конфигурации.
3. Сохраните необходимые шаги, запустите первую сборку master.
4. Поменяйте условия сборки: если сборка по ветке master, то должен происходит mvn clean deploy, иначе mvn clean test.
5. Для deploy будет необходимо загрузить settings.xml в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.
6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.
8. Мигрируйте build configuration в репозиторий.
9. Создайте отдельную ветку feature/add_reply в репозитории.
10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово hunter.
11. Дополните тест для нового метода на поиск слова hunter в новой реплике.
12. Сделайте push всех изменений в новую ветку репозитория.
13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.
14. Внесите изменения из произвольной ветки feature/add_reply в master через Merge.
15. Убедитесь, что нет собранного артефакта в сборке по ветке master.
16. Настройте конфигурацию так, чтобы она собирала .jar в артефакты сборки.
17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.
18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
19. В ответе пришлите ссылку на репозиторий.

---

Как оформить решение задания
Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

# Решение
Подготовка инфраструктуры
Создал ВМ в Yandex Cloud:
teamcity-server (4CPU/4RAM)
teamcity-agent (2CPU/4RAM)
Nexus (2CPU/4RAM)

![0000001-01](https://github.com/user-attachments/assets/a0defd67-e0fb-4c83-a1fe-b98af3d59016)

Настроил TeamCity: авторизовал агент, подключил репозиторий.

![0000001-02](https://github.com/user-attachments/assets/f8b9daf0-f99b-4099-af70-30e8c0e950a9)

Запустил Nexus через Ansible (плейбук из mnt-homeworks).

![0000001-03](https://github.com/user-attachments/assets/c7b73b41-92f3-4e9d-8a5e-1caac74e1975)

Настройка проекта
Сделал форк репозитория: ([https://github.com/aragastmatb/example-teamcity](https://github.com/aragastmatb/example-teamcity))
Склонировал на локальную машину

![0000001-04](https://github.com/user-attachments/assets/fc092fb5-8937-48da-8f95-d03d09ed32ef)

## Основная часть
Создал autodetect конфигурации и запустил сборку:

![0001 TeamCity](https://github.com/user-attachments/assets/27010e1a-77ba-48ff-ac05-bd1da24233a9)

![0002 TeamCity (самый первый билд)](https://github.com/user-attachments/assets/3aae6baf-7dcb-43eb-aac1-602d1e70cbc9)

Финальная конфигурация сборки

![0003-2 TeamCity (конфигнового Maven)](https://github.com/user-attachments/assets/b2b27d59-90b4-46a1-9c25-1d46083878c8)

![0004 TeamCity (Итоговая конфигурация)](https://github.com/user-attachments/assets/c140eee0-e14f-493f-980d-bd8c53c1df89)

![0005 TeamCity (Выполненый Build)](https://github.com/user-attachments/assets/38980493-8fd5-432b-8928-9e163b8a4e02)

Сборка по ветке feature/add_reply

![0006 TeamCity (RUN новой ветке в TeamCity)](https://github.com/user-attachments/assets/8af9c066-b3a3-4bb2-8f34-b36d5762690d)

Нновый метод для класса Welcomer

![0007 TeamCity (Задание с Git №9)](https://github.com/user-attachments/assets/ee72b931-5bef-4b64-bb4d-4df824af5017)

И тест для нового метода на поиск слова hunter

![0008 TeamCity (Задание с Git №9)](https://github.com/user-attachments/assets/44c62652-1514-43b4-ac9a-b57d4258c991)

Сборка прошла успешно и артефакты собраны

![0009 TeamCity  (последний скриншот)](https://github.com/user-attachments/assets/f19f1f2b-ada4-403d-8db4-521b658fcf22)

Ссылка на [репозитории](https://github.com/IlyaBridge/example-teamcity)

---
