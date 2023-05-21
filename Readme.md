*Создать свой RPM пакет
Подключаемся к виртуальной машине используя команду vagrant ssh 
Сменим пользователя на root, используя команду sudo -i
Для данного задания установим следующие пакеты ( используем команду yum install -y ): 
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/a9fb137e-c960-4acf-af3d-a31922a2089b)

* Для примера возьмем пакет NGINX и соберем его с поддержкой openssl
* Загрузим SRPM пакет NGINX для дальнейшей работý над ним ( используем команду wget):

![Снимок экрана от 2023-05-21 16-53-41](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/8d7c93ce-37df-4c03-8961-fea0418532a4)

*Установим текущий пакет в домашней дериктории :

![Снимок экрана от 2023-05-21 16-55-08](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/f91eaf8c-e2f2-4d37-89e8-3eed86d7736e)

*Скачаем исходники ssl (используем ключ --no-check-certificate, т.к. сертифкат сайта истек) :
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/358531b8-cf8b-477f-949d-0482778ca625)
 *Рзархивируем исходники ssl 
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/621f9e20-85a2-4d6a-8f66-01f0f9a72f9d)

*Заранее проставим все зависимости , что бы в процессе сборки не было ошибок:
 ![Снимок экрана от 2023-05-21 16-58-30](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/054827d0-0c23-4154-a14c-e5268770d262)

*Отредактируем  файл nginx.spec, указав путь до каталога openssl, в нашем случае это /root/openssl-1.1.1s
![Снимок экрана от 2023-05-21 17-01-02](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/52df8d70-bdc5-4f8f-875c-3e9ff98f0d93)
*Теперь приступим к сборке пакета :
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/962bcd1e-c894-452f-bdda-5257ca75fba1)
*Убедимся что пакеты были созданы :
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/22010e0d-110a-4fa0-bb2e-ca9efaeff192)
*Установим наш rpm  пакет и проверим что nginx работает( для этого используем команды systemctl start nginx ( запуск nginx) и команду systemctl status nginx( проверка что nginx работает)  :
![Снимок экрана от 2023-05-21 17-06-27](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/13799171-fe7a-4f24-a7ff-17038f514ed7)
* Из данного снимка мы видим, что  nginx имеет статус active(running) , что свидетельствует о том что nginx запущен.
![Снимок экрана от 2023-05-21 17-06-39](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/401306e7-e56d-4c0d-8a77-3a94231eff19)
* Узнаем ip адрес машины командой "ip a", как мы видим наша машина имеет адрес 192.168.56.101
![Снимок экрана от 2023-05-21 17-11-13](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/fc470200-2d4f-4031-8365-90588b74e2ca)
*Введем этот адрес в адресную строку браузера , что бы еще раз убедиться что веб сервер nginx запущен и работает 
![Снимок экрана от 2023-05-21 17-12-12](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/99ef5455-d3ed-4425-9369-ba2a81c33a02)
*Данный пакет мы будем использовать для размещения его в своем репозитории
2.Создать свой репозиторий и разместить там ранее собранный RPM
*Приступим к созданию собственного репозитория. По умолчанию nginx распологается в папке  /usr/share/nginx/html. Используя команду mkdir создадим там дерикторию repo
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/0e04ffe4-173d-4898-b0de-c997392ad18b)
* Используя команду cp копируем туда наш собранный RPM
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/644a10bf-b8d7-43ae-b469-65a6de0059ac)
*Скачиваем и в файл Persona-Server в папку с нашим rpm пакетом :
![Снимок экрана от 2023-05-21 17-23-21](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/5653e630-8bfa-46dc-9f6a-262e8277ee07)
* Используем команду createrepo для инициализации нашего репозитория
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/f0ece012-a33d-4974-8f38-6314f64a4f16)
*Как мы видим в 1 строке в нашем репозиотрии два пакета.
* Для прозрачности настроим в NGINX доступ к листингу каталога. Отредактируем файл default.conf, находящийся в директории /etc/nginx/conf.d/
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/77cd4ce6-8db5-4de8-b862-5d265a79214f)
*Добавим в этот файл директиву autoindex со значемнием "on"
![Снимок экрана от 2023-05-21 17-29-17](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/6173b973-56a6-4e0b-bdc3-87b45236db2a)

* Проверяем коректность конфигурационног файла командой nginx -t 
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/40d474dc-e411-44b5-a288-64617c8a6696)
* И перезапустим веб сервер командой nginx -s reload :
![изображение](https://github.com/AlexanderSerg-jun/vm_rpm/assets/85576634/efa82511-33cf-4bf3-8fda-9296c1715d86)






