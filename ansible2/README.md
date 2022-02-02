# Домашнее задание к занятию "8.2 Работа с Playbook"

Playbook запускает 3 Play:
1. Install Java
2. Install Elasticsearch
3. Install Kibana

Play **Install Java** выполняется для всех хостов. В нем выполняются следующие tasks:
- **Set facts for Java 11 vars** - устанавливается переменная `java_home` с помощью модуля `set_fact`.
- **Upload .tar.gz file containing binaries from local storage** - архив с JAVA копируется во в папку `/tmp/` с помощью модуля `copy`.
- **Ensure installation dir exists** - создание директории, указанной в переменной `java_home` с помощью модуля `file`.
- **Extract java in the installation directory** - распаковка архива с JAVA в созданную директорию с помощью модуля `unarchive`.
- **Export environment variables** - установка переменных окружения для JAVA с помощью модуля `template`.  
Переменные, которые используются в этом Play для всех хостов указаны в файле `group_vars/all/vars.yml`.

Play **Install Elasticsearch** выполняется для хостов, указанных в группе `elasticsearch`. В нем выполняются следующие tasks:
- **Upload tar.gz Elasticsearch from remote URL** - загрузка архива с Elasticsearch с помощью модуля `get_url`. В случае неудачной попытки, повторяет загрузку 3 раза.
- **Create directory for Elasticsearch** - создание директории, указанной в переменной `elastic_home` с помощью модуля `file`. Данная переменная указана в файле `group_vars/elasticsearch/vars.yml`
- **Extract Elasticsearch in the installation directory** - распаковка архива с Elasticsearch в созданную директорию с помощью модуля `unarchive`.
- **Set environment Elastic** - установка переменных окружения для Elasticsearch с помощью модуля `template`.  

Play **Install Elasticsearch** выполняется для хостов, указанных в группе `kbn`. В нем выполняются те же tasks, что и в Play **Install Elasticsearch**, только используются свои переменные, указанные в файле `group_vars/kbn/vars.yml`.

Кроме этого в Plays используются параметры `become` для возможности повышения привилегий пользователя при создании файлов и директорий и параметр `tags` для указания тэга для каждой task, чтобы была возможность выполнения tasks поотдельности.