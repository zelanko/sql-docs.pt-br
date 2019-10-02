---
title: azdata bdc spark batch reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc spark batch de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f37518ff2b53e80622c4a6faca477a08719c3dc
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708631"
---
# <a name="azdata-bdc-spark-batch"></a>bdc spark batch de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Commands
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
azdata bdc spark batch create --code "2+2"
```
### <a name="required-parameters"></a>Parâmetros necessários
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
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
azdata bdc spark batch list
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark batch info
Isso obtém as informações de um lote do Spark com a ID fornecida.  A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>Exemplos
Obter informações do lote com a ID 0.
```bash
azdata bdc spark batch info --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark batch log
Isso obtém as entradas de log do lote para um lote do Spark com a ID fornecida.  A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>Exemplos
Obter o log do lote com a ID 0.
```bash
azdata bdc spark batch log --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark batch state
Isso obtém o estado do lote para um lote do Spark com a ID fornecida.  A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>Exemplos
Obter informações de estado do lote com a ID 0.
```bash
azdata bdc spark batch state --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark batch delete
Isso exclui um lote do Spark. A ID do lote é retornada de 'spark batch create'.
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>Exemplos
Excluir um lote.
```bash
azdata bdc spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
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

- Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

- Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
