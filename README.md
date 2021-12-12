<h1 align="center">Соціальна мережа студентів та викладачів КПІ</h1>
<h2 align="center">

![alt text](pngs/kpi1.png "Найкращий університет країни!")

</h2>

<p align="center">
  
<img src="https://img.shields.io/badge/made%20by-%D0%A1%D1%96%D0%BD%2C%20%D0%9A%D0%B0%D1%81%60%D1%8F%D0%BD%D0%BE%D0%B2%D1%81%D1%8C%D0%BA%D0%B8%D0%B9%2C%20%D0%91%D1%94%D0%BB%D0%BE%D0%BA%D0%BE%D0%BF%D0%B8%D1%82%D0%BE%D0%B2%2C%20%D0%A7%D0%B5%D0%B1%D0%B0%D0%BA%D0%BE%D0%B2-blue">
  
<img src="https://img.shields.io/badge/faculty-FAM-red" >
  
<img src="https://img.shields.io/badge/group-KM--83-yellow" >
  
<img src="https://img.shields.io/badge/version-v1-green" >

<img src="https://badges.frapsoft.com/os/v1/open-source.svg?v=103" >

</p>

# Опис

**Наші цілі**</p>
Соціальна мережа студентів та викладачів КПІ створена задля того, аби забезпечити якісну комунікацію студентів та викладачів КПІ у
мережі інтернет та покращити якість та ефективність дистанційного навчання в КПІ.</p>

**Чому проект має бути**</p>
Створення даної мережі вирішує одразу декілька проблем, та сприяє розвиту університету!</p>
А саме:
- Бажання студентів та викладачів мати якісний рівень комунікаціїї
між собою в деякому окремому, стабільному та комфортному середовищі.
- Запровадженння дистанційної форми навчання в університеті.
- Відсутність діючої загальної стабільної та комфортної системи
комунікації між студентами та викладачами.
- Наявність схожих конкуруючих систем в інших університетах.
- Наявність всесвітньої практики створення окремої платформи для
комунікації між студентами та викладачами. 

**Як використовувати соціальну мережу**</p>
- Реєстрація користувача. Користувач повинен зареєструватися в
системі, щоб мати доступ до функції соціальної мережі та задати
потрібні дані: нікнейм, пароль, електронна пошта, ім’я, факультет,
кафедра, статус (викладач або студент), група (для студентів).
- Вхід до системи. Зареєстрованний користувач має війти до системи
після реєстрації або на іншому девайсі.
- Зміна даних профілю. Користувач може змінювати персональні данні
під час реєстрації та після неї.
- Відправка повідомлення. Користувач може відправляти особисті
повідомлення іншому користувачу, а також пости в канал, до якого
він має доступ.
- Приєднання до каналу. Користувач може приєднатися до каналу по
спеціальному посиланні або за запрошенням іншого користувача.
- Створення каналу. Користувач може створювати власні канали, до
яких може запрошувати інших користувачів.
- Коментування поста. Користувач має змогу користувати
пости в каналі, до якого він має доступ.

**Яими засобами було розроблено проект**</p>
- Для розробки серверної частини використовувати мову
програмування Python, бібліотеку Flask;
- Для розробки клієнтської частини використовувати мову
програмування JavaScript (TypeScript), бібліотеки ReactJS, Redux
Toolkit, Ant Design;
- Для реалізації live-чату використовувати технології websocket;
- Забезпечено доступ до мережі для не менш ніж 30 000 користувачів;
- Обмежено розмір відправлених файлів до 100 МБ;

# API</p>

## /api/session</p>
Методи: GET, POST, DELETE

**GET**</p>
*Перевіряє чи авторизований користувач.*</p>
Return: `{'data': {'id': int(cookies['uid'])}, 'errors': []}`

**POST**</p>
*Авторизувати користувача та встановлює cookie*</p>

Expected JSON request: `{
				‘login’: …,
				‘password: …
			}`</p>
Return: `{'data': {'id': user.uid}, 'errors': []}`

**DELETE**</p>
*Вийти з аккаунту користувача*</p>
Return: `{'data': {}}, 'errors': []}`

## /api/user/<int:uid></p>
Методи: GET, POST, PUT, DELETE</p>
Uid - id користувача (integer)

**GET**</p>
*Перевіряє чи авторизований користувач.*</p>
Return: `{'data': 
{'id': user.uid, 
'login': user.login,
'name': user.name,
'status': user.utype.name,
'photo': user.photo.path}, 'errors': []}`</p>
А також в залежності від user.utype.id повератає *department* та *group*

**POST**</p>
*Створити нового користувача та встановити cookie*</p>

Expected JSON request: `{
				‘login’: …,
				‘password: …, 
				‘Name’: …,
				‘Status’: ...
			}`</p>
Return: `{'data': {'id': new_user.uid}, 'errors': []}`

**DELETE**</p>
*Видалити користувача*</p>
Return: `{'data': {}}, 'errors': []}`

**PUT**</p>
*Оновити інформацію про користувача*</p>
Return: `{'data': {}}, 'errors': []}`

## /api/user/channels</p>
Методи: GET

**GET**</p>
*Отримати канали, на які підписаний користувач*</p>
Return: `{'data': {'items': items, 'total': len(items)}, 'errors': []}`

## /api/channel/<int:cid></p>
Методи: GET, PUT,POST, DELETE</p>
сid - id каналу (integer)

**GET**</p>
*Отримати інформацію про канал*</p>
Return: `{'data': 
{'id': channel.cid, 
'name': channel.name,
'description': channel.description,
'photo': channel.photo.path}, 'errors': []}`

**POST**</p>
*Створити новий канал*</p>
Return: `{'data': {'id': new_channel.cid}, 'errors': []}`

**DELETE**</p>
*Видалити користувача*</p>
Return: `{'data': {}}, 'errors': []}`

**PUT**</p>
*Оновити інформацію про канал*</p>
Return: `{'data': {}}, 'errors': []}`

## /api/channel/<int:cid>/members</p>
Методи: GET</p>
cid - id каналу

**GET**</p>
*Отримати список учасників каналу*</p>
Return: `{'data': {'items': items, 'total': len(items)}}, 'errors': []}`

## /api/channel/<int:cid>/posts</p>
Методи: GET</p>
cid - id каналу

**GET**</p>
*Отримати список постів даного каналу*</p>
Return: `{'data': {'items': items, 'total': len(items)}}, 'errors': []}`

## /api/posts/<int:pid></p>
Методи: GET, PUT,POST, DELETE</p>
pid - id посту

**GET**</p>
*Отримати інформацію про пост*</p>
Return: `{'data': data}, 'errors': []}`

**POST**</p>
*Створити новий канал*</p>
Expected JSON request: `{
				‘cid’: …
			}`</p>
Return: `{'data': {'id': new_post.id}, 'errors': []}`

## /api/uploads/<filename></p>
Методи: GET

**GET**</p>
*Доступ до статичного файлу filename*</p>

Return *файл з папкою static*

## /api/search?query=...&page=...&count=...
Методи: GET</p>
Page - номер сторінки (частини масиву)</p>
Count - кількість елементів на сторінці

**GET**</p>
*Пошук користувача по логіну або імені*</p>

Return: `{'data': {'items': items, 'total': total}, 'errors': []}`

## /api/user/contacts?page=...&count=...
Методи: GET

**GET**</p>
*Отримати контакти користувача*</p>

Return: `{'data': {'items': items, 'total': comtacts_count}, 'errors': []}`

## /api/contact/<int:contact_id>
contact_id - ID контакту</p>
Методи: POST, DELETE

**POST**</p>
*Додати новий контакт*</p>

Return: `{'data': {}, 'errors': []}`

**DELETE**</p>
*Видалити контакт*</p>

Return: `{'data': {}, 'errors': []}`

## /api/direct/<int:partner>?page=...&count=...
partner - ID партнера, з яким веде переписку поточний користувач</p>
Методи: GET

**GET**</p>
*Отримати дані переписки (повідомлення) між поточним користувачем та partner'ом*</p>

Return: `{'data': {'items': items, 'total': message_count}, 'errors': []}`

## /api/message
Методи: POST
**POST**</p>
*Надіслати повідомлення*</p>
Expected JSON request: `{
				‘receiverId’: …,
				‘text: …
			}`</p>

Return: `{'data': {'id': new_message.id}, 'errors': []}`


# База даних
*База  данних: PostgeSQL*</p>
*ORM: SQLALCHEMY*


# Тестування API</p>
**Опис**: тестування відбувається за використанням фреймворку pytest у файлі test_flask.py. Ми створюємо тестовий клієнт Flask'у, за допомогою якого відправляємо певний запит на сервер. Після отримання даних від серверу, ми перевіряємо оператором assert відповідність очікуваних та отриманих даних. Тести запускаються за допомогою команди pytest -v у папці з test_flaskr.py

## test_login(client)
Ендпоїнт, що перевіряється: /api/session</p>
Метод, що перевіряється: POST</p>
Тест №1:</p>
- Опис:*перевірка коректності авторизації користувача*</p>
- Дані для відправки: `{'login': 'NancyDye8533', 'password': 'NancyDye8533'}`</p>
- Очікувані дані: `{'data': {'id': ...}, 'errors': []}`
Тест №2:</p>
- Опис: *перевірка чи не буде сервер авторизовувати користувача з некоректними даними*</p>
- Дані для відправки: `{'login': 'invalid login', 'password': 'NancyDye8533'}`</p>
- Очікувані дані: `{'data': {},'errors': ['Invalid login or password']}`

## test_get_session(client)
Ендпоїнт, що перевіряється: /api/session</p>
Метод, що перевіряється: GET</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевірка чи коректно записується користувачу coockie*</p>
- Очікувані дані: `{'data': {'id': ...}, 'errors': []}`

## test_logout(client)
Ендпоїнт, що перевіряється: /api/session</p>
Метод, що перевіряється: DELETE</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевірка коректності виходу з аккаунту користувача*</p>
- Додатково перевіряємо, що coockie користувача дійсно видалені з сессії за допомогою `json.loads(client.get('/api/session').data)`</p>
- Очікувані дані: `{'data': {},'errors': ['No cookies']}`

## test_get_user(client)
Ендпоїнт, що перевіряється: /api/user/<int:uid></p>
uid = 1
Метод, що перевіряється: GET</p>
- Опис:*перевірка чи повертає сервер дані про користувача*</p>
- Очікувані дані: `{'data': {'id': ...},'errors': []}`

## test_create_user(client)
Ендпоїнт, що перевіряється: /api/user</p>
Метод, що перевіряється: POST</p>
Тест №1:</p>
- Опис:*перевірка чи коректно сервер створює користувача*</p>
- Дані для відправки: `{'login': 'logex', 'password': 'passex', 'name': "nameex", 'status': 'student'}`</p>
- Очікувані дані: `{'data': {'id': ...}, 'errors': []}`
Тест №2:</p>
- Опис: *перевірка чи не буде сервер створювати користувача з некоректними даними*</p>
- Дані для відправки: `{'login': 'logex', 'password': 'passex', 'name': "nameex", 'status': 'notstudent'}`</p>
- Очікувані дані: `{'data': {},'errors': ['Unknown user type']}`
Тест №3:</p>
- Опис: *перевірка чи не буде сервер створювати користувача з некоректними даними*</p>
- Дані для відправки: `{'login': 'logex', 'password': 'passex', 'name': "nameex"}`</p>
- Очікувані дані: `{'data': {},'errors': ['Bad request.']}`

## test_edit_user(client)
Ендпоїнт, що перевіряється: /api/user</p>
Метод, що перевіряється: PUT</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
Тест №1
- Опис:*первірка коректності поведінки серверу на запит про редагування юзера*</p>
- Дані для відправки: `{'name': "nameex", 'department': "departmentex", 'group': "groupex"}`</p>
- Очікувані дані: `{'data': {},'errors': []}`
Тест №2:
- Опис: *перевірка що name користувача дійсно було змінено*</p>
- Дані для відправки: `{'name': "nameex", 'department': "departmentex", 'group': "groupex"}`</p>
- Очікувані дані: `{'data': {'name': "nameex", ...},'errors': []}`

## test_get_user_channels(client)
Ендпоїнт, що перевіряється: /api/user/channels</p>
Метод, що перевіряється: GET</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевірка що сервер відправляє канали, в яких є користувач*</p>
- Очікувані дані: `{'data': {'items': items, ...},'errors': []}`

## test_get_channel(client)
Ендпоїнт, що перевіряється: /api/channel/<int:cid></p>
cid = 9
Метод, що перевіряється: GET</p>
Тест №1:</p>
- Опис:*перевірка чи повертає сервер коретну інформацію про канал*</p>
- Очікувані дані: `{'data': {'id': 1, ...}, 'errors': []}`
Тест №2:</p>
- Опис: *перевірка коректності поведінки серверу при запиті неіснуючого каналу*</p>
- Очікувані дані: `{'data': {},'errors': ['Channel not found']}`

## test_create_channel(client)
Ендпоїнт, що перевіряється: /api/channel</p>
Метод, що перевіряється: POST</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевірка чи коректно сервер створює канал*</p>
- Дані для відправки: `{'name': 'nameex', 'description': 'descex', 'members': [2, 3]}`</p>
- Очікувані дані: `{'data': {'id': ..., ...}, 'errors': []}`

## test_edit_channel(client)
Ендпоїнт, що перевіряється: /api/channel/<int:cid></p>
cid = 9
Метод, що перевіряється: PUT</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
Тест №1
- Опис:*первірка коректності поведінки серверу на запит про зміну каналу*</p>
- Дані для відправки: `{'name': 'nameex'}`</p>
- Очікувані дані: `{'data': {},'errors': []}`
Тест №2:
- Опис: *первірка коректності поведінки серверу на запит про зміну неіснуючого каналу, для цього передаємо в якості id каналу 999999*</p>
- Дані для відправки: `{'name': 'nameex'}`</p>
- Очікувані дані: `{'data': {},'errors': ['Channel not found']}`

## test_get_channel_posts(client)
Ендпоїнт, що перевіряється: /api/channel/<int:cid>/posts</p>
cid = 9
Метод, що перевіряється: GET</p>
- Опис:*перевірка чи повертає сервер коретну інформацію про канал*</p>
- Очікувані дані: `{'data': {'items': ..., ...},'errors': []}`

## test_get_post(client)
Ендпоїнт, що перевіряється: /api/posts/<int:pid></p>
pid = 1
Метод, що перевіряється: GET</p>
Тест №1
- Опис:*перевірка чи повертає сервер коретну інформацію про пост*</p>
- Очікувані дані: `{'data': {'id': ...},'errors': []}`
Тест №2:
- Опис: *перевірка коректності поведінки серверу при запиті неіснуючого посту, для цього передаємо в якості id поста 999999*</p>
- Очікувані дані: `{'data': {},'errors': ['Post not found']}`

## test_create_post(client)
Ендпоїнт, що перевіряється: /api/posts</p>
Метод, що перевіряється: POST</p>
Тест №1
- Опис:*перевірка чи коректно сервер створює пост*</p>
- Дані для відправки: `{'text': 'textex', 'channelId': 1}`</p>
- Очікувані дані: `{'data': {'id': ...},'errors': []}`
Тест №2:
- Опис: *перевірка чи не створює сервер пост з неіснуючим каналом*</p>
- Дані для відправки: `{'text': 'textex', 'channelId': 999999}`</p>
- Очікувані дані: `{'data': {},'errors': ['Specified channel does not exist']}`

## test_get_search(client)
Ендпоїнт, що перевіряється: /api/search</p>
Метод, що перевіряється: GET</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевіряє чи коректно сервер виконує пошук по користувачам, для цього передаємо запит query=Esther, щоб сервер повернув користовачів, чиє ім`я починаеться на 'Esther'*</p>
- Очікувані дані: `{'data': {'items': ..., ...},'errors': []}`

## test_get_user_contacts(client)
Ендпоїнт, що перевіряється: /api/user/contacts</p>
Метод, що перевіряється: GET</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевіряє чи коректно сервер отримує контакти користувача*</p>
- Очікувані дані: `{'data': {'items': ..., ...},'errors': []}`

## test_add_contact(client)
Ендпоїнт, що перевіряється: /api/contact/<int:contact_id></p>
contact_id = 2
Метод, що перевіряється: POST</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевіряє чи коректно сервер додає контакт до поточного користувача*</p>
- Очікувані дані: `{'data': {},'errors': []}`

## test_get_direct_massages(client)
Ендпоїнт, що перевіряється: /api/direct/<int:partner></p>
partner = 36
Метод, що перевіряється: GET</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевіряє чи коректно сервер отримує дані переписки (повідомлення) між поточним користувачем та partner'ом*</p>
- Очікувані дані: `{'data': {'items': ..., ...},'errors': []}`

## test_create_massage(client)
Ендпоїнт, що перевіряється: /api/message</p>
Метод, що перевіряється: POST</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевіряє чи коректно надсилає повідомлення*</p>
- Дані для відправки: `{'receiverId': 2, 'text': 'halo'}`</p>
- Очікувані дані: `{'data': {'id': ...},'errors': []}`

# Результати тестування API</p>

================================================= test session starts =================================================</p>
platform win32 -- Python 3.8.3, pytest-6.2.5, py-1.9.0, pluggy-0.13.1 -- c:\users\sinixy\appdata\local\programs\python\python38-32\python.exe</p>
cachedir: .pytest_cache</p>
rootdir: D:\AppMathOwO\7sem\DBIS\dbis_project_local</p>
plugins: dash-2.0.0</p>
collected 18 items</p>

test_flaskr.py::test_login PASSED                                                                                [  5%]</p>
test_flaskr.py::test_get_session PASSED                                                                          [ 11%]</p>
test_flaskr.py::test_logout PASSED                                                                               [ 16%]</p>
test_flaskr.py::test_get_user PASSED                                                                             [ 22%]</p>
test_flaskr.py::test_create_user PASSED                                                                          [ 27%]</p>
test_flaskr.py::test_edit_user PASSED                                                                            [ 33%]</p>
test_flaskr.py::test_get_user_channels PASSED                                                                    [ 38%]</p>
test_flaskr.py::test_get_channel PASSED                                                                          [ 44%]</p>
test_flaskr.py::test_create_channel PASSED                                                                       [ 50%]</p>
test_flaskr.py::test_edit_channel PASSED                                                                         [ 55%]</p>
test_flaskr.py::test_get_channel_posts PASSED                                                                    [ 61%]</p>
test_flaskr.py::test_get_post PASSED                                                                             [ 66%]</p>
test_flaskr.py::test_create_post PASSED                                                                          [ 72%]</p>
test_flaskr.py::test_get_search PASSED                                                                           [ 77%]</p>
test_flaskr.py::test_get_user_contacts PASSED                                                                    [ 83%]</p>
test_flaskr.py::test_add_contact PASSED                                                                          [ 88%]</p>
test_flaskr.py::test_get_direct_massages PASSED                                                                  [ 94%]</p>
test_flaskr.py::test_create_massage PASSED                                                                       [100%]</p>

================================================== warnings summary ===================================================</p>
kpi_network/test_flaskr.py::test_login</p>
  c:\users\sinixy\appdata\local\programs\python\python38-32\lib\site-packages\sqlalchemy\util\langhelpers.py:263: SADeprecationWarning: The 'postgres' dialect name has been </p>renamed to 'postgresql'</p>
    loader = self.auto_fn(name)</p>

-- Docs: https://docs.pytest.org/en/stable/warnings.html</p>
============================================ 18 passed, 1 warning in 0.93s ============================================</p>

