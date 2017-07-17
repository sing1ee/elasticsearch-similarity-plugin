# elasticsearch similarity plugin
custome similarity plugin for elasticsearch


### more details
- choose right version source code.
- run

```shell
gradle pz
```
- copy the zip file to plugin directory

```shell
cp build/distributions/simple-similarity-plugin-5.4.zip ${path.home}/plugins
```
- unzip and rm zip file

```shell
unzip simple-similarity-plugin-5.4.zip
rm simple-similarity-plugin-5.4.zip
```
- start elasticsearch

```shell
./bin/elasticsearch
```
### settgings

```shell
PUT http://localhost:9200/index
```

body:

```json
{
  "settings": {
  	"number_of_shards" :   2,
	"number_of_replicas" : 0,
    "index": {
      "similarity": {
        "mysim": {
          "type": "simple-similarity"
        }
      }
    }
  }
}
```

mappings:

```json
{
    "fulltext": {
             "_all": {
            "analyzer": "standard",
            "search_analyzer": "standard",
            "term_vector": "no",
            "store": "false"
        },
        "properties": {
            "content": {
                "type": "text",
                "store": "no",
                "similarity": "mysim",
                "term_vector": "with_positions_offsets",
                "analyzer": "standard",
                "search_analyzer": "standard",
                "include_in_all": "true",
                "boost": 8
            }
        }
    }
}
```
