# Лабораторная работа 1. 
## Знакомство с _IaaS_, _PaaS_, _SaaS_ сервисами в облаке на примере _Amazon Web Services (AWS)_. Создание сервисной модели.
### Цель работы: 

Знакомство с облачными сервисами. Понимание уровней абстракции над инфраструктурой в облаке. Формирование понимания типов потребления сервисов в сервисной-модели. 
### Дано: 
- Слепок данных биллинга от провайдера после небольшой обработки в виде _SQL_-параметров. Символ % в начале/конце означает, что перед/после него может стоять любой набор символов.
- Образец итогового соответствия, что желательно получить в конце. В этом же документе  
### Необходимо: 

1. Импортировать файл _.csv_ в _Excel_ или любую другую программу работы с таблицами. Для _Excel_ делается на вкладке Данные – Из текстового _.csv_ файла – выбрать файл, разделитель – точка с запятой.
2. Распределить потребление сервисов по иерархии, чтобы можно было провести анализ от большего к меньшему (напр. От всех вычислительных ресурсов _Compute_ дойти до конкретного типа использования - Выделенной стойка в датацентре _Dedicated host usage_).
3. Сохранить файл и залить в соответствующую папку на _Google Drive_.

### Алгоритм работы: 
Сопоставить входящие данные от провайдера с его же документацией. Написать в соответствие колонкам справа значения 5 колонок слева, которые бы однозначно классифицировали тип сервиса. Для столбцов _IT Tower_ и _Service Family_ значения можно выбрать из образца.
### 1. Знакомство с облачными сервисами. 
	
Если максимально обобщить, то облачные сервисы нужны нам для того, чтобы экономить
место на жестком диске, избавлять от необходимости носить флешку. Также они удобны
для обмена документами. 
 
### 2. Понимание уровней абстракции над инфраструктурой в облаке. 

![Image alt](0.png)

- _IaaS - Infrastructure-as-a-service_
  
Т.е. виртуальные машины, сетевые ресурсы и инфраструктурные элементы, облегчающие
эксплуатацию, например, балансировщики сетевой нагрузки. 

Также _IaaS_ можно описать, как низкоуровневый вариант администрирования, только с
виртуальной серверной.

- _PaaS - Platform-as-a-service_
  
Это возможность получить какое-то базовое ПО, запущенное и управляемое облаком, 
например, базы данных.

Также PaaS является хранилище _Amazon S3_.

- _SaaS - Software-as-a-service_
  
Т.е. _API_ или веб-интерфейс/ПО для доступа к приложению, которое он полностью 
поддерживает. Примером SaaS являются _GitHub_ и _Amazon SQS_.

### 3. Формирование понимания типов потребления сервисов в сервисной-модели. 
Далее шла работа со слепком биллинга. 

Для начала необходимо было, например,
в приложении _Excel_ по следущим шагам (Данные -> Получение внешних данных -> 
Из текста -> выбор файла -> с разделителями -> точка с запятой), импортировать
_.csv_ файлик. Подробнее можно увидеть на картинках 1-4. 

![Image alt](1.png)
![Image alt](2.png)
![Image alt](3.png)
![Image alt](4.png)

На картинке ниже табличка полученная в исходном виде. 

![Image alt](5.png)

В колонке `Product Code` представлены следующие сервисы:

`Amazon S3` - виртуальная СХД, доступ к которой возможен из любой точки, где есть 
интернет. Здесь _S3_ (_Simple Storage Service_) — протокол передачи данных, 
разработанный компанией Amazon. Также — объектное хранилище.

`Amazon Macie` - это сервис безопасности данных, который использует машинное 
обучение и сопоставление шаблонов для выявления конфиденциальных данных в 
Amazon S3, предоставляя информацию о рисках для безопасности и автоматизированную 
защиту.

`Amazon MSK` - это полностью управляемый сервис, который позволяет создавать и 
запускать приложения, использующие _Apache Kafka_ для обработки потоковых данных. 
Amazon MSK предоставляет операции уровня управления, например, для создания, 
обновления и удаления кластеров.

`Amazon Polly` - это сервис синтеза речи от AWS, который позволяет преобразовывать 
текст в естественную речь с использованием технологий глубокого обучения. 
Сервис способен автоматически интерпретировать распространенные текстовые форматы,
такие как сокращения, числовые последовательности и омографы.
Он поддерживает язык разметки синтеза речи (_SSML_) для настройки стиля речи и 
словари для индивидуального произношения. Сгенерированная `Amazon Polly` 
речь может быть экспортирована в формате _MP3_, _OGG_, с посткодовой модуляцией, 
речевыми знаками и т.д.

`Amazon Personalize` - это сервис персонализации пользовательского опыта в режиме 
реального времени, основанный на алгоритмах машинного обучения.
В основе `Amazon Personalize` лежит та же технология, что и в Amazon.com для 
персонализированных рекомендаций в режиме реального времени.

`Amazon ES - Amazon Elasticsearch Service` — это управляемый сервис, предлагаемый 
_AWS_, который упрощает развёртывание, защиту и масштабирование _Elasticsearch_ — 
популярной системы поиска и аналитики с открытым исходным кодом. 
Если подробнее, то _Elasticsearch_ — это распределённый механизм поиска и аналитики 
на основе _RESTful_, созданный на базе _Apache Lucene_. Он позволяет пользователям 
хранить, искать и анализировать большие объёмы данных в режиме реального времени.

### Итог
После анализа документации AWS, хабра и презенташек получилась вот такая табличка:
![Image alt](итогский.png)

В процессе выполнения лабораторной работы были закреплены знания уровней абстракции над инфраструктурой в облаке, сформировано примерное понимания типов потребления сервисов в сервисной-модели. Для себя запомнила сервис `Amazon Polly`, показался очень интересным, так что по возможности поизучаю побольше.

