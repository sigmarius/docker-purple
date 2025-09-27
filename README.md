# Мой репозиторий с ДЗ

Запуск контейнера с пробросом порта 8081 наружу с маппингом на порт 80 внутри  
`docker run --name dz-nginx -d -p 8081:80 dz-nginx:latest`  

curl с хостовой машины на порт 8081 вернет html
`curl http://localhost:8081`

## Postgres
`docker pull posgres` скачиваем image Postgres  
`docker run --name my-postgres -d -p 5433:5432 -v ~/data:/data/pg -e 
POSTGRES_PASSWORD=password postgres:latest`  
-- запускаем контейнер с именем `my-postgres` из скачанного образа  
-- пробрасываем порт 5433 с хоста на дефолтный порт postgres 5432 в контейнере  
-- биндим volume через Bind Mount из папки `/home/sigmarius/data` на хосте в папку `/data/pg` в контейере  

