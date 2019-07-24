---
title: referência de sessão do azdata BDC Spark
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de sessão do azdata BDC Spark.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20b7ac3dcf72482e80278ce0f0df922026232a6d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426096"
---
# <a name="azdata-bdc-spark-session"></a>sessão do Spark do azdata BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

O artigo a seguir fornece referência para os comandos de **sessão do BDC Spark** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[criação de sessão do azdata BDC Spark](#azdata-bdc-spark-session-create) | Crie uma nova sessão do Spark.
[lista de sessões do azdata BDC Spark](#azdata-bdc-spark-session-list) | Listar todas as sessões ativas no Spark.
[informações da sessão do Spark do azdata BDC](#azdata-bdc-spark-session-info) | Obter informações sobre uma sessão ativa do Spark.
[log de sessão do azdata BDC Spark](#azdata-bdc-spark-session-log) | Obter logs de execução para uma sessão ativa do Spark.
[Estado de sessão do azdata BDC Spark](#azdata-bdc-spark-session-state) | Obter estado de execução para uma sessão ativa do Spark.
[exclusão da sessão do azdata BDC Spark](#azdata-bdc-spark-session-delete) | Excluir uma sessão do Spark.
## <a name="azdata-bdc-spark-session-create"></a>criação de sessão do azdata BDC Spark
Isso cria uma nova sessão interativa do Spark. O chamador deve especificar o tipo de sessão do Spark. Esta sessão fica além do tempo de vida de uma execução de azdata e deve ser excluída com ' exclusão de sessão do Spark '
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
Crie uma sessão.
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--session-kind -k`
Nome do tipo de sessão a ser criado.  Um dos Spark, pyspark, sparkr ou SQL.
#### `--jar-files -j`
Lista de caminhos de arquivo jar.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--py-files -p`
Lista de caminhos de arquivo do Python.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--files -f`
Lista de caminhos de arquivo.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--driver-memory`
Quantidade de memória a ser alocada ao driver.  Especifique as unidades como parte do valor.  Exemplo 512M ou 2G.
#### `--driver-cores`
Quantidade de núcleos de CPU a serem alocados ao driver.
#### `--executor-memory`
Quantidade de memória a ser alocada ao executor.  Especifique as unidades como parte do valor.  Exemplo 512M ou 2G.
#### `--executor-cores`
Quantidade de núcleos de CPU a serem alocados ao executor.
#### `--executor-count`
Número de instâncias do executor a serem executadas.
#### `--archives -a`
Lista de caminhos de arquivos mortos.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--queue -q`
Nome da fila do Spark na qual executar a sessão.
#### `--name -n`
Nome da sessão do Spark.
#### `--config -c`
Lista de pares de valor de nome que contêm valores de configuração do Spark.  Codificado como dicionário JSON.  Exemplo: ' {"Name": "value", "nome2": "value2"} '.
#### `--timeout-seconds -t`
Tempo limite de ociosidade da sessão em segundos.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-list"></a>lista de sessões do azdata BDC Spark
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
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-info"></a>informações da sessão do Spark do azdata BDC
Isso obtém as informações da sessão para uma sessão ativa do Spark com a ID fornecida.  A ID da sessão é retornada de ' Spark Session Create '.
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>Exemplos
Obter informações de sessão para a sessão com ID 0.
```bash
azdata spark session info --session-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-log"></a>log de sessão do azdata BDC Spark
Isso obtém as entradas de log de sessão para uma sessão do Spark ativa com a ID fornecida.  A ID da sessão é retornada de ' Spark Session Create '.
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>Exemplos
Obter o log de sessão para a sessão com ID 0.
```bash
azdata spark session log --session-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-state"></a>Estado de sessão do azdata BDC Spark
Isso Obtém o estado da sessão para uma sessão do Spark ativa com a ID fornecida.  A ID da sessão é retornada de ' Spark Session Create '.
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>Exemplos
Obter estado de sessão para a sessão com ID 0.
```bash
azdata spark session state --session-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-spark-session-delete"></a>exclusão da sessão do azdata BDC Spark
Isso exclui uma sessão interativa do Spark. A ID da sessão é retornada de ' Spark Session Create '.
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>Exemplos
Excluir uma sessão.
```bash
azdata spark session delete --session-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).
