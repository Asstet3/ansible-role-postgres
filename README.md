Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------
postgres_pg_1c true or false - Задает будте ли установлен postgrespro-1c или винильный

postgres_pg_ver 15 - Указываем версию пострегсса которую хотим установить

postgres_db_data: "/data/pgbase" - Путь к каталогу, где будут создавать директории с кластерами постргрес

postgres_db_dir: [prod,prod3] - Список директорий которые будут созданы в postgres_db_data, так же будут называться службы postgreespro-1c

postgres_db_locale: "ru_RU.UTF-8 " - требуемая локаль при инициализации базы данных

postgres_db_init_command_1c: "/opt/pgpro/1c-{{ postgres_pg_ver }}/bin/initdb "  - путь дошinitdb, если postgres_pg_1c true

postgres_db_init_command: "/usr/lib/postgresql/{{ postgres_pg_ver }}/bin/initdb" - путь до ванильной

postgres_db_checksum: "true" - по умолчанию инициализирует кластер с проверкой контрольных сумм

postgres_db_extra_opt: "--auth-local=trust --auth-host=scram-sha-256 " - параметры аутентификации при инициализации БД

postgres_db_ports: [5432,5433] - Список портов которые будут прописаны в postgresql.conf после инициализации

postgres_db_user: false  - Нужно ли менять пароль у пользователя postgres

postgres_db_user_pass: "Qwerty" - если postgres_db_user: true назначить пользователю этот пароль

postgres_db_rep_slot: false - ## true только для мастера!!! 
Создает пользователя из переменной postgres_db_rep_role с паролем postgres_db_rep_role
Так же добавляет в  pg_hba.conf запись разрешающую подключения созданного пользователя для репликации.

postgres_db_rep_pgpass: false -  Создает pgpass файл(Копирует из шаблона /var/lib/postgresql/.pgpass) pgpass если true!!!! Перезатирает старый

postgres_db_rep_size: 3GB  - Задает значение wal_keep_size

inventory_replica_ip: 127.0.0.1 - Задает ip адресс хоста к которому будет подключаться для репликации(Задавать в inventory)

inventory_replica_host: "{{ ansible_facts['nodename'] }}" - указывает primary_slot_name

inventory_replica_signal -  если TRUE, то зайдет в replica.yml. Проверит существование standby.signal в директориях баз дданных. Создать со слейва бекап(мастера)  и сразуже подключится для асинхронной репликации.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
