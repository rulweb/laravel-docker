## Моя конфигурация Laravel Docker

Кидаем в папку с Laravel проектом 

### Для сборки выполняем следующую команду

```bash
docker-compose build
```

### И после запустить

```bash
docker-compose up -d
```

Флаг `-d` говорит о том, что контейнеры будут запущены в фономов режиме

### Можно собирать и запустить одной командой

```bash
docker-compose up --build -d
```

### Для остановки контейнеров используем

```bash
docker-compose stop
```

### Для удаления контейнеров

```bash
docker-compose down
```