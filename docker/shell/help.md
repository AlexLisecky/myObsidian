# Команды докера

Запустить docker-compose.yml

	docker-compose up

Запустить docker-compose.yml сразу с сборкой

	docker-compose up --build

Запустить docker-compose.yml в фоновом режиме(в консоли не будет логов)

	docker-compose up -d

Удалить все не связянные с контейнерами ресурсы(Images, toms, networks)

	docker system prune

Удалить все ресурсы 

	docker system prune -a
