---
title: azdata bdc spark batch reference
description: Artigo de referência para comandos bdc spark batch de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d141669313a90bd04cda2e54d5a9e9d5a3c68f6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258630"
---
# <a name="azdata-bdc-spark-batch"></a>bdc spark batch de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `bdc spark batch` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc spark batch create](#azdata-bdc-spark-batch-create) | Criar um novo lote do Spark.
[azdata bdc spark batch list](#azdata-bdc-spark-batch-list) | Listar todos os lotes no Spark.
[azdata bdc spark batch info](#azdata-bdc-spark-batch-info) | Obter informações sobre um lote ativo do Spark.
[azdata bdc spark batch log](#azdata-bdc-spark-batch-log) | Obter logs de execução para um lote do Spark.
[azdata bdc spark batch state](#azdata-bdc-spark-batch-state) | Obter o estado de execução para um lote do Spark.
[azdata bdc spark batch delete](#azdata-bdc-spark-batch-delete) | Excluir um lote do Spark.
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark batch create
Isso cria um novo trabalho do Spark em lote que executa o código fornecido.
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              [--arguments -a]  
                              [--jar-files -j]  
                              [--py-files -p]  
                              [--files]  
                              [--driver-memory]  
                              [--driver-cores]  
                              [--executor-memory]  
                              [--executor-cores]  
                              [--executor-count]  
                              [--archives]  
                              [--queue -q]  
                              [--name -n]  
                              [--config]
```
### <a name="examples"></a>Exemplos
Criar um novo lote do Spark.
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--file -f`
Caminho para o arquivo a ser executado.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--class-name -c`
Nome da classe a ser executada ao passar um ou mais arquivos jar.
#### `--arguments -a`
Lista de argumentos.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--jar-files -j`
Lista de caminhos de arquivo jar.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--py-files -p`
Lista de caminhos de arquivo python.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--files`
Lista de caminhos de arquivo.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--driver-memory`
Quantidade de memória a ser alocada ao driver.  Especifique as unidades como parte do valor.  Por exemplo, 512M ou 2G.
#### `--driver-cores`
Quantidade de núcleos de CPU a ser alocada ao driver.
#### `--executor-memory`
Quantidade de memória a ser alocada ao executor.  Especifique as unidades como parte do valor.  Por exemplo, 512M ou 2G.
#### `--executor-cores`
Quantidade de núcleos de CPU a ser alocada ao executor.
#### `--executor-count`
Número de instâncias do executor a serem executadas.
#### `--archives`
Lista de caminhos de arquivos.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--queue -q`
Nome da fila do Spark na qual executar a sessão.
#### `--name -n`
Nome da sessão do Spark.
#### `--config`
Lista de pares de nome e valor que contêm valores de configuração do Spark.  Codificado como um dicionário JSON.  Exemplo: '{"nome":"valor", "nome2":"valor2"}'.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark batch list
Listar todos os lotes no Spark.
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>Exemplos
Listar todos os lotes ativos.
```bash
azdata spark batch list
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark batch info
Isso obtém as informações de um lote do Spark com a ID fornecida.  A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch info --batch-id -i 
          ```
### Examples
Get batch info for batch with ID of 0.
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--batch-id -i`
Número da ID do lote do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark batch log
Isso obtém as entradas de log do lote para um lote do Spark com a ID fornecida.  A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch log --batch-id -i 
         ```
### Examples
Get batch log for batch with ID of 0.
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--batch-id -i`
Número da ID do lote do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark batch state
Isso obtém o estado do lote para um lote do Spark com a ID fornecida.  A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch state --batch-id -i 
           ```
### Examples
Get batch state for batch with ID of 0.
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--batch-id -i`
Número da ID do lote do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark batch delete
Isso exclui um lote do Spark. A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch delete --batch-id -i 
            ```
### Examples
Delete a batch.
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--batch-id -i`
Número da ID do lote do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
