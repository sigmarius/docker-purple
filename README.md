# Мой репозиторий с ДЗ

Запуск контейнера с пробросом порта 8081 наружу с маппингом на порт 80 внутри  
`docker run --name dz-nginx -d -p 8081:80 dz-nginx:latest`  

curl с хостовой машины на порт 8081 вернет html
`curl http://localhost:8081`

## Postgres
`docker pull posgres` скачиваем image Postgres  
`docker run --name my-postgres -d -p 5433:5432 -v /home/vasa/data:/data/pg -e 
POSTGRES_PASSWORD=password postgres:latest`  
-- запускаем контейнер с именем `my-postgres` из скачанного образа  
-- пробрасываем порт 5433 с хоста на дефолтный порт postgres 5432 в контейнере  
-- биндим volume через Bind Mount из папки `/home/vasa/data` на хосте в папку `/data/pg` в контейере  

`docker rm -f my-postgres` удаляет контейнер без удаления volume  
`ll /home/vasa/data` просматриваем содержимое папки на хосте - оно на месте  
`mkdir test` создаем новую папку для хранения данных  
`sudo mv data test/data` переносим папку с данными на хосте в новую папку test  
`docker run --name my-postgres -d -p 5433:5432 -v /home/test/vasa/data:/data/pg -e
POSTGRES_PASSWORD=password postgres:latest` снова запускаем контейнер - данные с хоста на месте  

## Ansible Roles
### Задача
Написать роль для создания пользователей:  
- Проходится по массиву имён пользователей и их паролей  
- Создаёт для каждого пользователя  
- Генерит публичный и приватный ключ  
- Кладёт публичную часть в authorized_keys  
- Добавляется всех пользователей в группу docker  
#### Требования:
- Проходит ansible-lint  
- vault.yml с паролями должен быть зашифрован  
### Решение:
- Файл с необходимыми коллекциями для роли: requirements.txt
`ansible-galaxy install -r requirements` установка зависимостей из файла  
- Запуск плейбука для роли  
`ansible-playbook -i inventory all.yml --vault-id dev@.vault-pass`
