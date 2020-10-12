[ABOUT PROGRAM]

Это система предназначается для учета печати. 

Система состоит из сущностей:

    ● Администратор;
    ● Дилер;
    ● Пользователь;
    ● Плоттер;
    ● Лекало.

Администратор имеет полный доступ ко всем пользователям,
товарам, плоттерам и может просматривать статистику по ним.
Администратор имеет возможность добавления, редактирования и
удаления:

    ● Дилеров;
    ● Плоттеров;
    ● Лекал.

Дилер имеет доступ к своим пользователям, которых добавил,
статистике своих пользователей и плоттеров.
Дилер добавляет и редактирует:

    ● Пользователей;
    ● Плоттеры.
   
Пользователь имеет доступ к своим плоттерам и их
статистике, может вырезать разрешенное кол-во копий лекал из
пленки.

[REQUIREMENTS]
В самом начале нам необходимо выполнить миграции командами:

docker-compose run web python manage.py makemigrations

и 

docker-compose run web python manage.py migrate

Создайте superuser командой:

docker-compose run web python manage.py createsuperuser

Введите Username и Password который в дальнейшем.

Далее вы можете запустить сервер командой:
 
docker-compose up

Эти две команды установят все необходимые зависимости.

[USAGE]

После запуска перейдите на страницу входа: http://localhost:8000/api/authlogin/
Введите логин и пароль, который вы использовали при создании суперпользователя.

В данный момент вам доступны все возможности.

Для разграничения прав доступа используются встроенные группы в нашем приложении, такие как:

    1. administrator
    2. dealer
    3. user

Права для каждой группы соответсвуют требованиям из описания приложения.
Также хочу заметить, что при обычной регистрации пользователей, их будут автоматически определять в группу 'user'.

Для того что бы зарегистировать пользователя и определить его в группу 'administrator',
необходимо сделать сдедующие шаги:

    1. Зарегистрировать пользователя по ссылке http://localhost:8000/api/v1/user/registration/
        1.1 В POST форме заполните поля: Username, First name, Email, Password.
    2. Перейти по ссылке http://localhost:8000/admin/
    3. Ввести логин и пароль суперюзера.
    4. Кликнуть на 'Users' 
    5. В списке найти и кликнуть пользователя которого требуется определить в группу 'administrator'.
    6. В параметрах Groups выбрать 'administrator' одним кликом, начнет подсвечиваться синим цветом.
    7. Колесиком мышки прокручиваем в самый низ страницы и нажимаем на кнопку 'Save' в правом нижнем углу.
    8. Поздравляю, вы справились.

При добавлении администратором дилера, его группа будет автоматически определена.

При добавлении дилером пользователя, его группа и параметр dealer_id(который обозначает дилера, который добавил пользователя), так же будут автоматически определены.

На главной странице http://localhost:8000/api/v1/ - вы обнаружите все конечные точки нашего API.

Внутри страниц с данными пользователей, плоттеров и лекал, вы обнаружите конечные точки для редактирования, удаления и изменения конкретного объекта.
 