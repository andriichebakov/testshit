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
Тестування відбувається за використанням фреймворку pytest у файлі test_flask.py. Ми створюємо тестовий клієнт Flask'у, за допомогою якого відправляємо певний запит на сервер. Після отримання даних від серверу, ми перевіряємо оператором assert відповідність очікуваних та отриманих даних.

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
Метод, що перевіряється: GET</p>
Для коректної роботи спочатку авторизовуємо користувача: `client.post('/api/session',  json={'login': 'NancyDye8533', 'password': 'NancyDye8533'})`</p>
- Опис:*перевірка чи коректно записується користувачу coockie*</p>
- Очікувані дані: `{'data': {'id': ...}, 'errors': []}`




