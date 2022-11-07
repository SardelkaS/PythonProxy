# PythonProxy

![alt text](https://github.com/SSA-hub/PythonProxy/blob/master/image.png)

HTTP прокси сервер, равномерно распределяющий нагрузку между сервисами.  
Адреса веб-сервисов задаются в файле proxy/src/appsettings.json  
Прокси сервер работает на хосте http://localhost:8000/ и принимает Get-запрос, который перенаправляет другому сервису.  

#### Развертка
Proxy - proxy/Dockerfile
Target - target/Dockerfile
Файл docker-compose.yaml поднимает 1 прокси и 5 таргет сервисов, каждый в отдельном контейнере  

#### Ответы прокси-сервера
1) "Hello, world!" (status_code = 200) - нормальный ответ  
2) "All servers is off" (status_code = 500) - все сервисы-обработчики не отвечают  

#### Тестирование  
Можно запустить файл run.ps1, который выполнит следующие действия:  
1) Поднимает прокси и 5 таргет сервисов  
2) Запустит скрипт spamer.py, который отправляет Get-запрос на прокси-сервер каждые 0.2 секунды  
3) Через 100 секунд остановит 3-й таргер-сервис  
4) Еще через 100 секунд запустит 3-й таргет-сервис снова  
  
В файле test/testing_locust.py содержится скрипт для запуска locust, его можно запустить следующей командой:  
py -m locust -f testing_locust.py --host=http://localhost:8000  
Далее перейти по адресу http://localhost:8089/ и задать параметры тестирования.
