# Union

Типы Union очень похожи на интерфейсы, но они не могут 
указывать какие-либо поля между типами объектами, 
а объединяют несколько разных объектов в одном типе.

```graphql
union SearchResult = Article | User
```

Где бы мы ни возвращали тип `SearchResult` в нашей схеме, 
мы могли бы получить `Article` или `User`. 
Обратите внимание, что члены `Union` типа объединения 
должны быть конкретными типами объектов. Вы не можете 
создать `Union`, содержащий `Interface` или другой `Union`.

Если вы запрашиваете поле, которое возвращает тип 
`SearchResult`, вам нужно использовать условный фрагмент, 
чтобы иметь возможность запрашивать любые поля:

```graphql
{
    search(text: "hello world") {
        ... on Article {
            name
        }
        ... on User {
            name
        }
    }
}
```