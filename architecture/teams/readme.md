# Teams
JuJa связка состоит из 4х участников , не важно с каким опытом ребята. Цель - взаимная поддержка и контроль участников связки для окончания тренига.

## Технические характеристики проекта:

* JDK8
* Mongo
* SpringBoot
* SpringData
* SpringMVC
* jUnit
* FakeMongo 
* LordOfTheJars

## Общие положения:
**TMF-D1** Хранитель - особенный тип пользователей, которые занимаются активной поддержкой и развитием определенных направлений на курсе.

**TMF-D2** Связка состоит из 4х человек. Один человек может состоять только в одной связке.

**TMF-D3** Участники выбираются вручную.

**TMF-D4** В случае отсутствия активности связка расформировывается. Максимальный срок жизни связки - 1 мес.

**TMF-D5** В случае успешно выполненной операции для void методов юзер получает ответ 200 OK. “void метод” - это endpoint который не подразумевает возврата результата. Смотри детальнее [тут](https://ru.wikipedia.org/wiki/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2_%D1%81%D0%BE%D1%81%D1%82%D0%BE%D1%8F%D0%BD%D0%B8%D1%8F_HTTP#200)

### TMF-F1
***TMF-F1 Я как хранитель хочу иметь возможность создавать связки. Связка это команда состоящая из четырех человек.***

* TMF-F1-D1 Операцию могут выполнять не все пользователи. Только хранители TMF-D1.
* TMF-F1-D2 Хранитель в комманде указывает четырех пользователей, будущих участников связки.
* TMF-F1-D3 Необходимо проверять чтобы пользователь не состоял уже в другой связке.
* TMF-F1-D4 Номер для связки определяется инкрементом для наибольшего существующего номера связки в БД.

* TMF-F1-URL
```
    url - "/teams"
    method - POST
```
* TMF-F1-REQ
```
    {
        "from" : "...",
        "user1" : "...",
        "user2" : "...",
        "user3" : "...",
        "user4" : "..."
    }
```
* TMF-F1-RSP["..."] - один элемент в массиве(id - номер сформированой комманды)

### TMF-F2
***TMF-F2 Я как хранитель хочу иметь возможность расформировывать связки.***

* TMF-F2-D1 Операцию могут выполнять не все пользователи. Только хранители TMF-D1.
* TMF-F2-D2 Хранитель указывает id связки которую необходимо расформировать.

* TMF-F2-URL
```
    url - "/teams/{id}"
    method - PUT
```
* TMF-F2-REQ
```
    {
        "from" : "..."
    }
```
* TMF-F2-RSP["..."] - один элемент в массиве(id - номер расформированой комманды)

### TMF-F3
***TMF-F3 Я как пользователь хочу иметь возможность получить список всех связок с id и участниками.***

* TMF-F3-D1 Операцию может выполнить любой пользователь.
* TMF-F3-D2 Результатом выполнения этой комманды должен быть список, содержащий в себе все активные связки с id и участниками.

* TMF-F3-URL
```
    url - "/teams"
    method - GET
```
* TMF-F3-REQ
```
   {}
```
* TMF-F3-RSP
```
    [
    {
    "id": .... ,
    "members": [uuid1, uuid2, uuid3, uuid4],
    "start": date,
    "finish": date
    }
    ]
```
### TMF-F4
***TMF-F4 Я как пользователь хочу иметь возможность получить список всех участников определенной связки.***

* TMF-F4-D1 Операцию может выполнить любой пользователь.
* TMF-F4-D2 Результатом выполнения этой команды должен быть список, содержащий в себе uuid всех участников выбранной связки 
 или текст ошибки.  

* TMF-F4-URL
```
    url - "/teams/{id} //id связки
    method - GET
```
* TMF-F4-REQ
```
    {}
```
* TMF-F4-RSP
```
        {
        "id": .... ,
        "members":[uuid1, uuid2, uuid3, uuid4]
        }
 - id команды и uuid ее участников 
```

### TMF-F5
***TMF-F5 Я как пользователь хочу иметь возможность получить список всех участников своей активной связки.***

* TMF-F5-D1 Операцию может выполнить любой пользователь.
* TMF-F5-D2 Результатом выполнения этой команды должен быть список, содержащий в себе uuid всех участников связки текущего пользователя или текст ошибки.  

* TMF-F5-URL
```
    url - "/teams/myteam/{uuid} //uuid пользователя, по которому ищется свяка
    method - GET
```
* TMF-F5-REQ
```
    {}
```
* TMF-F5-RSP
```
        {
        "id": .... ,
        "members":[uuid1, uuid2, uuid3, uuid4]
        }
 - id команды и uuid ее участников 
```