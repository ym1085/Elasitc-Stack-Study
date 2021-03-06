## ๐ Elastic Stack

![https://user-images.githubusercontent.com/53969142/148395221-ce7cae37-b5de-46c1-9c9a-de58fa6722a8.PNG](https://user-images.githubusercontent.com/53969142/148395221-ce7cae37-b5de-46c1-9c9a-de58fa6722a8.PNG)

## ๋ชฉ์ฐจ

1. ์๋ผ์คํฑ์์น CRUD
2. RDBMS์ ์์ธ
3. ์๋ผ์คํฑ ์์น์ ์์ธ
4. ๋ถ์๊ธฐ

## ๐ ์๋ผ์คํฑ์์น CRUD

| ๋ฉ์๋ | ์ค๋ช               | ๋ฉ์๋ 1 | ์ค๋ช 1             |
| ------ | ------------------ | -------- | ------------------ |
| POST   | ํด๋น ๋ฆฌ์์ค๋ฅผ ์ถ๊ฐ | GET      | ํด๋น ๋ฆฌ์์ค๋ฅผ ์กฐํ |
| PUT    | ํด๋น ๋ฆฌ์์ค๋ฅผ ์์  | DELETE   | ํด๋น ๋ฆฌ์์ค๋ฅผ ์ญ์  |

- **์๋ผ์คํฑ์์น๋ ๋ชจ๋  ์์ฒญ๊ณผ ์๋ต์ REST API ํํ๋ก ์ ๊ณต**
- 6.x ๋ถํฐ PUT๊ณผ POST๋ฅผ ์๊ฒฉํ ๊ตฌ๋ถํ์ง ์๊ณ  ์ฌ์ฉ์ ํ๋ค.

### RESTFul API

![https://user-images.githubusercontent.com/53969142/148395354-6f5da10c-e0b5-4ea7-9828-8955f5dc9e98.PNG](https://user-images.githubusercontent.com/53969142/148395354-6f5da10c-e0b5-4ea7-9828-8955f5dc9e98.PNG)

**Restful API**๋ฅผ ํตํด index์ document๋ฅผ ์ถ๊ฐํ  ์ ์๋๋ฐ,
์ด๋ฌํ ์์์ **๋ฌธ์๋ฅผ ์์ธํ** ํ๋ค ์ง์นญ

### ์ธ๋ฑ์ค ๋ง๋ค๊ธฐ

```
PUT customer?pretty

```

- **PUT ๋ฉ์๋**๋ฅผ ์ฌ์ฉํ์ฌ **customer**๋ผ๋ **์์ธ**์ ์์ฑ
- **pretty**์ ๊ฒฝ์ฐ reponse(๊ฒฐ๊ณผ)๋ฅผ ์์๊ฒ ๋ณด์ฌ์ฃผ๊ธฐ ์ํจ

```
{
  "acknowledged": true, // ์๋ต ๊ฒฐ๊ณผ ์ฌ๋ถ
  "shards_acknowledged": true, // ํ์ํ ์์ shard copy์ ์์ ์ ๋ฌด
  "index": "customer" // ์์ฑ๋ ๋ฐ์ดํฐ ๋ฒ ์ด์ค(์ธ๋ฑ์ค)๋ช
}
```

### ์ธ๋ฑ์ค ์กฐํ

```
GET /_cat/indices?v
```

- **GET**: HTTP ๋ฉ์๋๋ช
- **\_cat**: ์๋ผ์คํฑ์์น์์ ์ ๊ณตํด์ฃผ๋ API
- **indices**: ๋ณต์์ ์ธ๋ฑ์ค๋ฅผ ์๋ฏธ

```
health status index                             uuid                   pri rep docs.count docs.deleted store.size pri.store.size
yellow open   filebeat-7.16.2-2021.12.23-000001 _vAVYsNlT5OBFWhrZl2N4w   1   1          0            0       226b           226b
green  open   .geoip_databases                  pX5UN4wESS-vCV5AoEuhxQ   1   0         44           43     43.6mb         43.6mb
green  open   .kibana_task_manager_7.16.2_001   JwZwWmBvQv20SgLrQainDw   1   0         17         5733      1.8mb          1.8mb

```

### ์๋ผ์คํฑ ์์น์์ ์ ๊ณตํ๋ API

```
## _์ธ๋๋ฐ                            : API๋ฅผ ์๋ฏธ
## _cat/health?v                     : ํ์ฌ ํด๋ฌ์คํฐ์ ์ํ
## _cat/nodes?v                      : ๋ธ๋ ์ํ
## _update                           : ํน์  ๋ฐ์ดํฐ ์๋ฐ์ดํธ
## _search                           : ๋ฐ์ดํฐ ์ ์ฒด ์กฐํ
## ?v                                : ์์ธ ์ ๋ณด ํ์ธ
```

- ๊ธฐ๋ณธ์ ์ผ๋ก ์์ฃผ ์ฌ์ฉ์ด ๋๋ API ๋ฆฌ์คํธ

### ๋ฐ์ดํฐ ์ฝ์

```
POST tourcompany/customerlist/1
{
  "name": "Alfred",
  "phone": "010-1234-5678",
  "holiday_dest": "Disneyland",
  "departure_date": "2017/01/20"
}
```

- **index**: tourcompany
- **type**: customerlist
- **id**: 1

### ๋ฐ์ดํฐ ์ฝ์ ์ฑ๊ณต

```
{
  "_index" : "customer",
  "_type" : "type1",
  "_id" : "1", ## document => ์ง์ ํ์ง ์์ ์ ๋๋ค์ผ๋ก ๋ค์ด๊ฐ๋ค
  "_version" : 1,
  "result" : "created",
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 0,
  "_primary_term" : 1
}
```

### ๋ฐ์ดํฐ ์ญ์ 

```
DELETE customer/type1/1

```

- ๋ฐ์ดํฐ ์ญ์  ์ **์ธ๋ฑ์ค**, **ํ์**, **Id**๋ฅผ ์ง์ 
- POST์๋ ๋ค๋ฅด๊ฒ **๋ฐ๋ ์์ญ**์ด ์กด์ฌํ์ง ์๋๋ค.

### ๋ฐ์ดํฐ ์ญ์  ์ฑ๊ณต

```
{
  "_index" : "customer",
  "_type" : "type1",
  "_id" : "1",
  "_version" : 2,
  "result" : "deleted", # ์ญ์  ์ฌ๋ถ
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "_seq_no" : 1,
  "_primary_term" : 1
}
```

### ๋ฐ์ดํฐ ์์ 

```
# ์๋ ๋ช๋ น์ด๋ฅผ ํตํด document์ ์ผ๋ถ๋ถ์ ๋ณ๊ฒฝํ  ์ ์๋ค
POST customer/type1/1/_update
{
  "doc" : {
    "age" : 123
  }
}

# ํด๋น ๋ช๋ น์ด๋ document ์ ์ฒด๋ฅผ ๊ฐ์๋ผ์ฐ๋ ๋ฐฉ๋ฒ
POST customer/type1/1
{
  "name": "ymkim"
}
```

## ๐ RDBMS์ ์์ธ

![https://user-images.githubusercontent.com/53969142/148395526-a627bf8f-f0ff-4826-b17b-e1b1616b7ce5.jpg](https://user-images.githubusercontent.com/53969142/148395526-a627bf8f-f0ff-4826-b17b-e1b1616b7ce5.jpg)

- **MySQL**, **MS-SQL**, **MariaDB** ๋ฑ๋ฑ

### โ  ์ผ๋ฐ์ ์ธ ๋ฐ์ดํฐ๋ฒ ์ด์ค ์ธ๋ฑ์ฑ(Indexing)

![https://user-images.githubusercontent.com/53969142/148395566-d1f99c80-775b-47a1-9f3f-9e412b8d9612.PNG](https://user-images.githubusercontent.com/53969142/148395566-d1f99c80-775b-47a1-9f3f-9e412b8d9612.PNG)

- ์ผ๋ฐ์ ์ธ ๋ฐ์ดํฐ๋ฒ ์ด์ค(MySQL, MS-SQL)๋ **๋จ๋ฐฉํฅ ์์ธ**์ ์ฌ์ฉ
- ๋ํ์ ์ผ๋ก **Like ๊ฒ์**์ ์ฌ์ฉ

### โก ์ผ๋ฐ์ ์ธ ๋ฐ์ดํฐ๋ฒ ์ด์ค ์ธ๋ฑ์ฑ(Indexing)

![https://user-images.githubusercontent.com/53969142/148395596-44f04fc4-130e-401f-a132-2cdc60698e68.PNG](https://user-images.githubusercontent.com/53969142/148395596-44f04fc4-130e-401f-a132-2cdc60698e68.PNG)

- **ํน์  ํค์๋**๋ฅผ ์ฐพ๊ธฐ ์ํด์๋ **Full Scan**์ ์ํ ํด์ผํ๋ค
- **์๋จํ ์ฐ์ฐ**์ ์๋ฐ
- **๋ณ๋์ ์บ์ฑ ๋ก์ง**์ ์ถ๊ฐํ์ง ์๋ ์ด์ **๊ฐ์ ์์์ ๋ฐ๋ณต**

## ๐ ์๋ผ์คํฑ ์์น์ ์์ธ?

![https://user-images.githubusercontent.com/53969142/148395793-7c210024-4675-4f86-9507-0d3d46700929.PNG](https://user-images.githubusercontent.com/53969142/148395793-7c210024-4675-4f86-9507-0d3d46700929.PNG)

- ์๋ผ์คํฑ ์์น๋ ๊ธฐ๋ณธ์ ์ผ๋ก **์ญ์์ธ**์ ์ฌ์ฉํ๋ค

### โ  [์๋ผ์คํฑ ์์น์ ์ญ์์ธ](https://jiseok-woo.tistory.com/3)

![https://user-images.githubusercontent.com/53969142/148395847-5e6905cb-4785-4aa9-b515-5cf23f554cc5.PNG](https://user-images.githubusercontent.com/53969142/148395847-5e6905cb-4785-4aa9-b515-5cf23f554cc5.PNG)

1. ์๋ผ์คํฑ ์์น๋ ๋ฐ์ดํฐ ์ ์ฅ ์ ์๋ฏธ์๋ **๋จ์ด๋ค์ ์ถ์ถ**
2. ํด๋น ๋จ์ด๋ค๋ก ์ญ์์ธ(Inverted Index)๋ฅผ ์์ฑ
3. ๋จ์ด๋ฅผ ๊ฒ์์ **์ด๋ค ๋ํ๋จผํธ**์ **ํด๋น ๋จ์ด๊ฐ ํฌํจ๋ ์๋์ง** ํ์ธ ๊ฐ๋ฅ

### โก ์๋ผ์คํฑ ์์น์ ์ญ์์ธ

![https://user-images.githubusercontent.com/53969142/148395886-7071520b-2030-4e80-a5b3-aef588d59460.PNG](https://user-images.githubusercontent.com/53969142/148395886-7071520b-2030-4e80-a5b3-aef588d59460.PNG)

- ๋ฐ์ดํฐ๊ฐ ๋์ด๋๋ ์ฐพ์๊ฐ์ผ ํ  ํ์ด ๋์ด๋๋ ๊ฒ์ด ์๋๋ผ `์ญ ์ธ๋ฑ์ค๊ฐ ๊ฐ๋ฆฌํค๋ id์ ๋ฐฐ์ด๊ฐ์ด ์ถ๊ฐ๋๋ ๊ฒ ๋ฟ`์ด๊ธฐ ๋๋ฌธ์ ํฐ ์๋์ ์ ํ ์์ด ๋น ๋ฅธ ์๋๋ก ๊ฒ์์ด ๊ฐ๋ฅํฉ๋๋ค

## ๐ ๋ถ์๊ธฐ?

![https://user-images.githubusercontent.com/53969142/148396342-1bf7d99d-b566-4cba-927b-d654da04c009.PNG](https://user-images.githubusercontent.com/53969142/148396342-1bf7d99d-b566-4cba-927b-d654da04c009.PNG)

### โ  ๋ถ์์ ํ์ํ ๊ตฌ์ฑ ์์

#### ์ ์ฒ๋ฆฌ ํํฐ - CharFilters

- ์๋ฌธ์์ ๋ถํ์ํ ๋ฌธ์๋ฅผ ์ ๊ฑฐํ๋ค
- ๋ฌธ์์ด ์์ฒด๊ฐ ๋ถ๋ฆฌ๋๊ฒ์ด ์๋, ํํฐ๋ง ๋ ๋ฌธ์์ด

### โก ๋ถ์์ ํ์ํ ๊ตฌ์ฑ ์์

#### ํ ํฌ๋์ด์  ํํฐ ๋ฌธ์ ๋ถ๋ฆฌ ๋ฐฉ๋ฒ

- **standard tokenizer**
  - ๊ธฐํธ ๊ธฐ์ค
- **whitespace tokenizer**
  - ๊ณต๋ฐฑ ๊ธฐ์ค
- **ngram tokenizer**
  - ํ ๊ธ์์ฉ
- **keyword tokenizer**
  - ๋ถ๋ฆฌํ์ง ์๋๋ค

### โข ๋ถ์์ ํ์ํ ๊ตฌ์ฑ ์์

#### ํ ํฐ ํํฐ

- **Ascii Folding**
  - ASCII
- **Lowercase**
  - ์๋ฌธ์
- **Uppercase**
  - ๋๋ฌธ์
- **Stop**
  - ๋ถ์ฉ์ด ์ฌ์ ์ ๊ตฌ์ถํ์ฌ ๊ฒ์๋์ง ์์ ๋จ์ด ์ง์ 
- **Synonym**
  - **๋์์ด ์ฒ๋ฆฌ**๋ฅผ ์ํ ํํฐ, ๋น์ทํ ๋ป์ผ๋ก ์ฐ์ด๋ ๋จ์ด๋ฅผ ๋ฌถ๋๋ค
  - ex) ์ ํ ๊ฒ์ โ ์์ดํฐ ๊ฒ์ ๊ฒฐ๊ณผ๋ฅผ ํฌํจํ์ฌ ํ์
- **Trim**
  - ๊ณต๋ ์ ๊ฑฐ

### ์ฐธ๊ณ  ์๋ฃ

- [Elasticsearch ๊ฐ๋ฐ๋ถํฐ ์ด์๊น์ง](http://www.yes24.com/Product/Goods/103030516) ๐
- [6.1 ์ญ ์ธ๋ฑ์ค - Inverted Index](https://esbook.kimjmin.net/06-text-analysis/6.1-indexing-data)
- [6.2 ํ์คํธ ๋ถ์ - Text Analysis](https://esbook.kimjmin.net/06-text-analysis/6.2-text-analysis)
- [Character filters reference](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-charfilters.html)
- [Elasticsearch ๋ถ์](https://nesoy.github.io/articles/2019-03/ElasticSearch-Analysis)
- [Analysis & Analyzer](https://u2ful.tistory.com/28)
