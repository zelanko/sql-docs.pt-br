---
title: azdata bdc spark session reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc spark session de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6b4001a18cbc609a6eaccd634e029b22d90f02a
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243507"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark session

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descrição |
| --- | --- |
[azdata bdc spark session create](#azdata-bdc-spark-session-create) | Criar uma nova sessão do Spark.
[azdata bdc spark session list](#azdata-bdc-spark-session-list) | Listar todas as sessões ativas no Spark.
[azdata bdc spark session info](#azdata-bdc-spark-session-info) | Obter informações sobre uma sessão ativa do Spark.
[azdata bdc spark session log](#azdata-bdc-spark-session-log) | Obter logs de execução para uma sessão ativa do Spark.
[azdata bdc spark session state](#azdata-bdc-spark-session-state) | Obter estado de execução para uma sessão ativa do Spark.
[azdata bdc spark session delete](#azdata-bdc-spark-session-delete) | Excluir uma sessão do Spark.
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark session create
Isso cria uma nova sessão interativa do Spark. O chamador deve especificar o tipo de sessão do Spark. Esta sessão dura além do tempo de vida de uma execução de azdata e deve ser excluída usando 'spark session delete'
```bash
azdata bdc spark session create [--session-kind -k] 
                                [--jar-files -j]  
                                
[--py-files -p]  
                                
[--files -f]  
                                
[--driver-memory]  
                                
[--driver-cores]  
                                
[--executor-memory]  
                                
[--executor-cores]  
                                
[--executor-count]  
                                
[--archives -a]  
                                
[--queue -q]  
                                
[--name -n]  
                                
[--config -c]  
                                
[--timeout-seconds -t]
```
### <a name="examples"></a>Exemplos
Criar uma sessão.
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--session-kind -k`
Nome do tipo de sessão a ser criada.  Uma opção entre spark, pyspark, sparkr ou sql.
#### `--jar-files -j`
Lista de caminhos de arquivo jar.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--py-files -p`
Lista de caminhos de arquivo python.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--files -f`
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
#### `--archives -a`
Lista de caminhos de arquivos.  Para passar o JSON de uma lista, codifique os valores.  Exemplo: '["entrada1", "entrada2"]'.
#### `--queue -q`
Nome da fila do Spark na qual executar a sessão.
#### `--name -n`
Nome da sessão do Spark.
#### `--config -c`
Lista de pares de nome e valor que contêm valores de configuração do Spark.  Codificado como um dicionário JSON.  Exemplo: '{"nome":"valor", "nome2":"valor2"}'.
#### `--timeout-seconds -t`
Tempo limite de ociosidade da sessão em segundos.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark session list
Listar todas as sessões ativas no Spark.
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>Exemplos
Listar todas as sessões ativas.
```bash
azdata spark session list
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark session info
Isso obtém as informações da sessão para uma sessão ativa do Spark com a ID fornecida.  A ID da sessão é retornada usando 'spark session create'.
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>Exemplos
Obter informações da sessão com a ID 0.
```bash
azdata spark session info --session-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark session log
Isso obtém as entradas de log da sessão para uma sessão ativa do Spark com a ID fornecida.  A ID da sessão é retornada usando 'spark session create'.
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>Exemplos
Obter o log de sessão para a sessão com a ID 0.
```bash
azdata spark session log --session-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark session state
Isso obtém o estado de sessão para uma sessão ativa do Spark com a ID fornecida.  A ID da sessão é retornada usando 'spark session create'.
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>Exemplos
Obter o estado de sessão para a sessão com a ID 0.
```bash
azdata spark session state --session-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark session delete
Isso exclui uma sessão interativa do Spark. A ID da sessão é retornada usando 'spark session create'.
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>Exemplos
Excluir uma sessão.
```bash
azdata spark session delete --session-id 0
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
