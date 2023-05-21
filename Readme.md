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



