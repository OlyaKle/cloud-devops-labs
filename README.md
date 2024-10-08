# DevOps-lab2
### Подготовка к выполнению заданий
С помощью команды `touch` создаём файл под названием `Dockerfile`:
```
touch Dockerfile
```
Далее с помощью команды `ls` можно проверить результат:

![Image alt](1.png)

## Задание 1
> Написать “плохой” Dockerfile, в котором есть не менее трех “bad practices”.
При реализации были "допущены" следующие плохие практики:

- **тег _latest_**
  ```
  FROM ubuntu:latest
  ```
Он не означает «последний созданный». Это тег по умолчанию, который используется, 
если указывать имя образа без тега.

*Тэг не динамичен*. Если вытолкнуть новое изображение с тегом, который не является 
пустым или «latest», тег «latest» не будет затронут или создан. 

*Его легко перезаписать*. Любой разработчик, который не предоставляет тег образа, 
может непреднамеренно перезаписать изображение с тегом «latest». 

*С ним сложно работать*. Если работать с образом, помеченным «latest», это будет вся 
информация, кроме идентификатора образа. 

*Использование политики always pull policy* вместе с тэгом «latest» может привести к 
непредсказуемому результату. Если за время работы образ с тэгом «latest» в 
репозитории изменился, в новом Pod будет образ, который отличается от образов в 
остальных Pod этого Deployment. 

- **каждая команда с новой строки**
  ```
  RUN apt-get update
  RUN apt-get install -y cowsay fortune
  ```
Награмождение слоёв влечет за собой повреждение файловой системы внутри контейнера. Слишком много слоёв могут 
добавить или удалить файл или каталог, что загромождает файловую систему.

- **загрузка неиспользуемых приложений** - отсуствие экономии места, замедление сборки образа.
```
RUN apt-get -y install libpq-dev imagemagick gsfonts ruby-full
```
Пример такого файла представлен на картинке:

![Image alt](7.png)

Пример работы с таким докерфайлом представлен на следующих двух картинках:

![Image alt](8.png)
![Image alt](9.png)
## Задание 2
> Написать “хороший” Dockerfile.

В исходном "плохом" докерфайле был исправлен тег базового образа с неоднозначного `latest` на `24.04`, то бишь последней версии из онлайн документации установленной версии ubuntu.
```
 FROM ubuntu:24.04
```
Строки с обновлением и установкой необходимых приложений были аккуратно объединены, с использованием разделительного символа `&&`:
```
RUN apt-get update && apt-get install -y cowsay fortune
```
Строка с установкой неиспользующегося приложения была соответственно удалена. Получившийся "хороший" Dockerfile можно у видеть на картинке ниже:

![Image alt](10.png)

На следкющей картинке видно, что работа с приложением происходит корректно.

![Image alt](11.png)

## Задание 3
> Описать 2 плохих практики по работе с контейнерами.

Ошибки при работе с контейнерами:
- _конфликт имён_

К примеру, иногда при создании контейнера пользователи пытаются использовать имя, которое ранее было присвоено другому контейнеру в этой системе. 

- _использование sudo при каждой команде_

Её в принципе можно использовать только в крайних случаях, так как она раскрывает слишком много доступа, и для этого стоит проверить доступ к контейнеру, и если его нет, то настроить, следующими командами:
```
groups
```
Таким образом мы проверим существующие группы,
```
sudo groupadd docker
```
Этой командой можно создать группу, если её ещё не существует,
```
sudo usermod -aG docker olya
```
Теперь изменён доступ юзера `olya` к докерфайлу,
```
newgrp docker
```
А последней командой мы переключились на новую группу, в которой юзер точно состоит. Результат на фото.

![Image alt](12.png)
