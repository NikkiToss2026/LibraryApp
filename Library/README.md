Library application

Сеть веб-приложений, автоматизирующая работу библиотечной системы — от управления филиалами и складом до обслуживания читателей — вместе со встроенным банковским приложением «Кварц Банк», через которое проходят все денежные операции внутри экосистемы.

### Возможности

**Для администрирования**
Суперадминистратор каждой системы (библиотеки и банка) управляет базой данных напрямую через интерфейс: редактирует записи во всех таблицах, меняет структуру таблиц без обращения к файлам, видит наглядную ERD-схему связей между данными. У суперадминистратора библиотеки есть встроенная система публикаций — раздел FAQ и новости системы, которые заполняются и редактируются прямо на сайте.

**Для сети филиалов**
Склад принимает и обрабатывает заявки филиалов на пополнение и возврат книг с подтверждением и комментарием к решению. Сотрудники филиалов ведут бронирование, выдачу и возврат книг, отслеживают доступность экземпляров и состояние фонда, работают с архивом списанных изданий.

**Для читателей**
Каталог с фильтрами по автору, названию, филиалу и жанру. Бронирование бумажных книг, аренда электронных книг и аудиокниг на выбранный срок с сохранением прогресса чтения и прослушивания, личный кабинет с историей броней и активных аренд.

**Банковское приложение**
Отдельная система расчётов: клиенты управляют своими счетами и картами, переводят и пополняют средства, обращаются в поддержку через тикет-систему. Сотрудники банка обслуживают операции по счетам, обрабатывают обращения клиентов. Все платежи внутри библиотечной сети (аренда электронных изданий) автоматически проводятся через банк.

### Архитектура

Два полностью независимых приложения внутри одного проекта — у каждого своя база данных, свой сервер и собственная логика, без общего кода между ними. Серверная часть написана на чистом Python поверх сырого TCP-сокета — без веб-фреймворков: сервер сам разбирает HTTP-запросы и формирует ответы. Каждое действие проходит двойную проверку — на клиенте и на сервере.

Каждая роль в системе — суперадминистратор, склад, сотрудники, читатели, клиенты и сотрудники банка — работает со своим набором страниц и своим портом, при этом один серверный процесс обслуживает все роли своей системы целиком.

### База данных

Библиотека и банк ведут каждая свою базу данных в формате JSON — с полным описанием схемы таблиц и связей между ними. Это не статичный дамп: суперадминистратор работает с данными и структурой таблиц напрямую через сайт, и любое изменение — правка записи, добавление строки, изменение структуры таблицы — сразу же применяется к самому файлу базы данных на сервере.




A network of web applications that automates a library system — from managing branches and the warehouse to serving readers — together with a built-in banking application, "Kvarts Bank", that handles every monetary operation inside the ecosystem.

### Features

**Administration**
The superadmin of each system (library and bank) manages the database directly through the interface: edits records in every table, changes table structure without touching any files, and sees a clear ERD-style diagram of the relationships between data. The library superadmin also has a built-in publishing system — an FAQ and news section that's written and edited right on the site.

**Branch network**
The warehouse receives and processes branch requests for restocking and returning books, approving or rejecting each one with a comment. Branch staff handle reservations, checkouts and returns, track copy availability and book condition, and manage the archive of decommissioned titles.

**Readers**
A catalog with filters by author, title, branch and genre. Reserving physical books, renting e-books and audiobooks for a chosen period with reading/listening progress saved, and a personal account with a history of reservations and active rentals.

**Banking application**
A separate settlement system: customers manage their accounts and cards, transfer and deposit funds, and reach support through a ticketing system. Bank staff handle account operations and respond to customer requests. All payments within the library network (e-book and audiobook rentals) are automatically processed through the bank.

### Architecture

Two fully independent applications live inside one project — each with its own database, its own server, and its own logic, with no shared code between them. The server is written in plain Python on top of a raw TCP socket — no web framework: it parses HTTP requests and builds HTTP responses by hand. Every action is validated twice — once on the client and once on the server.

Each role in the system — superadmin, warehouse, staff, readers, bank customers and bank staff — works with its own set of pages and its own port, while a single server process serves every role of its own system.

### Database

The library and the bank each keep their own database as a JSON file, with a full description of table schemas and the relationships between them. It isn't a static dump: the superadmin works with the data and the table structure directly through the site, and any change — editing a record, adding a row, altering a table's structure — is applied to the database file on the server immediately.
