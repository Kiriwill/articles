## Diferenças do mapeamento objeto-relacional entre Django e Flask

Flask é um micro-framework, isto é, contém só as funções essenciais para a construção de API’s REST e desenvolvimento web. Ele é versátil e flexível, porém precisa de outras ferramentas para construir aplicações escaláveis. Para executar o mapeamento objeto relacional (ORM, sigla em inglês), portanto, é necessário instalar bibliotecas auxiliares como sqlAlchemy ou plugins como flask-sqlalchemy. Todas as rotinas de atualização dos modelos (migration) precisam ser construidas manualmente ou com auxilio de outras dependencias.

No codigo abaixo, mostro um exemplo de ORM para uma tabela Item com os atributos id, nome e valor unitário:

```python
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class Item(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(24), nullable=False)
    unit_value = db.Column(db.Numeric(precision=5, scale=2), nullable=False)
```

Uma diferença dessa stack é que é preciso lidar manualmente com as sessões, o que no caso do Django é feito automaticamente. Em alguns casos isso pode dar mais controle da aplicação já você pode controlar todos os passos das dependencias, pastas, etc.

Para inserir um item, então, é preciso declarar expressamente a sessão que as alterações devem ser realizadas (comando "commit"):

```python
def insert_row(Table:str, **kwargs):

    row = Table(**kwargs)
    db.session.add(row)
    db.session.commit()

    logger.info(f'{Table} inserido.')
```

A função *insert_row* insere uma linha na classe Table e depois executa a alteração (commit). 

Django, no entanto é um framework que vem com boa parte dos recursos necessários para construir aplicações web. Ele fornece um modulo interno para lidar com operações de ORM atraves de classes próprias.

```python
from django.db import models

class Item(models.Model):
    id = models.IntegerField(primary_key=True)
    name = models.CharField(max_length=30)
    unit_value = models.IntegerField()
```
e para atualizar os dados:

```python
item = Item()
item.name = "Novo Item 1"
record.save()
```

A primeira diferença é que ele já fornece uma arquitetura da aplicação por meio de comandos como o ```django-admin startproject nomedoprojeto```. Dentro da pasta do projeto é criado um arquivo de migração (migration.py) e outro de modelos (model.py). Assim, quando um modelo é modificado o Django rastreia as mudanças e automaticamente migra a nova estrutura para o banco de dados. Isso pode ser executado também pela linha de comando interna como pelo comando ```python3 manage.py migrate```.
 

