### Como você estruturaria a extração de relatórios CSV a partir de uma coleção de dezenas de milhares de documentos JSON armazenados externamente?

Tendo em vista a construção de uma arquitetura de microserviços hospedada na Cloud AWS estruturaria a extração como um repositório a parte. Utilizaria Python como linguagem, o Django como *framework* e o modelo *Model View Controller* com a seguinte estrutura:

```
nomeprojeto-documentos/
    manage.py
    locallibrary/
    app/
        __init__.py
        migrations/
            migrations.py
        models/
            model_name.py
        services/
            extractor_service.py
            conversor_service.py
        views/
            views.py
        tests/
            test_name.py
        admin.py
        error_handler.py
        cloud_handler.py
        apps.py
```

Os arquivos handler, correspondem ao tratamento de erros genérico para as APIs e a inicialização das instancias da Cloud (biblioteca `boto3`). 

As APIs estariam na pasta views. A API `get_documents()` extrairia o documento do banco (método GET) e a API `get_report()` requisita o documento e transforma o mesmo documento em CSV e o armazena no S3 (método POST). O serviço de extração do documento do banco e o serviço de conversão do Json para csv estariam em módulos separados para aumentar a reusabilidade. 

Para extrair, construiria funções com o papel de filtrar os dados e as organizaria por tipo de dado. Os filtros estariam conforme segue:
- Dados numericos:
    - por quantidade de produção;
    - por preço unitário.
- Strings:
    - por data (timestamp);
    - por organização;
    - por atividade fim (produto);
    - tipo de produto.
            
Para converter, o serviço receberia os dados da filtragem como parâmetro da função. Através da biblioteca nativa `csv` executaria a conversão.

Por fim os dados seriam gravados no S3 partir sob o caminho *{bucket}/relatorios/{nome_organizacao}/{nome_do_projeto}*. 
Um novo relatório só é armazenado de 15 em 15 minutos. O objetivo é guardar a versão dos documentos e evitar múltiplas requisições desnecessárias. 







Arquitetura de microserviços com MCV em Django:
- projeto proprio "Extração relatório CSV"
- contendo apis:
    - GET documento: extrai documento Dynamo (servico);
        - filtros por:
            - por data (dia, ano, horario);
            - por autor (pessoa);
            - por organização;
            - atividade fim (produto);
            - keyword (script para gerar esse campo);
            - qtde produção;
            - tipo de produto (in natura, artesanal, processado, etc)
            - preço unitário;
        - Serializar para objetos Python;
        - Armazenar em lista;
    - GET relatorio csv/documento (id): requisita doc (servico) e transforma json em CSV (servico);
        - importar lib csv nativa;
