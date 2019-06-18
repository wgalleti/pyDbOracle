# pyDbOracle

Está lib foi desenvolvida para facilitar o dia a dia de quem precisa martelar comandos a moda antiga (SELECT, UPDATE, INSERT) em bancos oracle.

## Instalação

```
pip install pyDbOracle
```

## Utilização

Alguns exemplos de uso.

### Conexão básica

```Python
from pyDbOracle.database import Database
str_conn = 'oracle://<USER>:<PASS>@<HOST>:<PORT>/<INSTANCE>'
db = Database(str_conn)
db.info()
```


### Conexão em banco com RAC

```Python
from pyDbOracle.database import Database
str_conn = 'oracle://<USER>:<PASS>@<HOST>:<PORT>/<INSTANCE>?threaded=True'
db = Database(str_conn)
db.info()
```


### Conexão definindo charset

```Python
from pyDbOracle.database import Database
str_conn = 'oracle://<USER>:<PASS>@<HOST>:<PORT>/<INSTANCE>?encoding=utf-8'
db = Database(str_conn)
db.info()
```

### Executando queries

```Python
from pyDbOracle.database import Database
str_conn = 'oracle://<USER>:<PASS>@<HOST>:<PORT>/<INSTANCE>'
db = Database(str_conn)
command = 'SELECT INSTANCE_NAME FROM V$INSTANCE'
data = db.get(command=command)
print(data)
# {'instance_name': 'PROD'}
```

### Executando queries com filtros

```Python
from pyDbOracle.database import Database
str_conn = 'oracle://<USER>:<PASS>@<HOST>:<PORT>/<INSTANCE>'
db = Database(str_conn)
command = 'SELECT INSTANCE_NAME FROM V$INSTANCE WHERE HOST = :host'
params = dict(host='MEUHOST')
data = db.get(command=command, params=params)
print(data)
# {'instance_name': 'PROD'}
```

### Executandos Inserts, Updates ou Deletes

Quando precisar executar um comando do tipo insert, update ou delete, rodar o metodo `run` 

```Python
from pyDbOracle.database import Database
str_conn = 'oracle://<USER>:<PASS>@<HOST>:<PORT>/<INSTANCE>'
db = Database(str_conn)
command = 'INSERT INTO TABELA (COLUNA1, COLUNA2) VALUES (:valor1, :valor2)'
params = dict(valor1='ABC', valor2=123)
data = db.run(command=command, params=params)
print(data)
# 1
```
