# Тут будут болтаться файлики по диссеру
---

## Структура хранения

### data - файлы для модели / храения данных
### data/concepts - файлы с информацией об объектах 

#### Для каждого отдельного элемента существует папка в data/concepts/, где название папки - код элемента, а название файлов внутри отражает текущую версию информации в базе


Это ссылки на текущую онтологию, не трогаем:
```json
{
    "@context":{
        "ex":"https://example.org/ontology/",//path to ontology
        "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
        "rdfs": "http://www.w3.org/2000/01/rdf-schema#"
    },
}
``` 


```json
{
    "@id": "https://corp.example.org/concepts/#ID/#VERSION",
    "@type": "#TYPE"
    }
```
  

`@id` - путь до файла (без расширения файла), где #ID - код элемента, а #VERSION - его ревизия  
`@type` - тип объекта (пока что только строительные конструкции, будет обновляться по мере обработки таблиц)


```json
{
    "ex:uid": "#UID",
    "ex:version": "#VERSION",
    "ex:status": "#STATUS", //  relevant/outdated
    "rdfs:label": "#NAME",
    "rdfs:comment": "#DESCRIPTION"
    }
```
  

`uid` - уникальный идентификатор (на текущий момент #ID+#VERSION)  
`version` - ревизия объекта  
`status` - статус информации (актуально/не актуально), указывается `relevant`/`outdated`  
`label` - название объекта текстом  
`comment` - описание объекта, если есть  


```json
{
    "rdfs:subClassOf": {
        "@id": "https://corp.example.org/concepts/#PARENTID"
    },
}
```

`subClassOf` - подклассом чего является объект  
`@id` - @id родительского класса, пишется в #PARENTID  

```json
{
    "ex:classification": {
        "@type": "ex:ClassificationCode",
        "ex:system": "KSI",
        "ex:table": "#TABLE",
        "ex:code": "#ID"
    },
}
```

`classification` - классификационная таблица  
`system` - система, по которой классифицируется, пока что только КСИ  
`table` - таблица по КСИ  
`code` - код по КСМИ  

```json
{
    "ex:externalLinks": [
        {
            "ex:system": "",
            "ex:code": ""
        }
    ],
}
```
 
`externalLinks` - внешние классификаторы (может быть enum)  
`system` - система классификации  
`code` - код по классификатору (раздел классификатора)  

```json
{
    "ex:source": [
        {
        "@type": "ex:RegulatoryDocument",
        "ex:title": "#TITLE",
        "ex:date": "#DATE", //format yyyy-mm-dd
        "ex:number": "#NUMBER"
        }
    ]
}
```

`source` -  норматинвые документы (может быть enum)  
`@type` - тип документа  
`title` - наименование документа  
`date` - дата принятия документа  
`number` - номер документа  