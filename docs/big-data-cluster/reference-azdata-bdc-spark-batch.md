---
title: referência de lote do azdata BDC Spark
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de lote do azdata BDC Spark.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6e242b26f439b49dbf0b3cf5ab50ea46c273f45f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426156"
---
# <a name="azdata-bdc-spark-batch"></a>lote do Spark no azdata BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos do **lote do Spark no BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[criação de lote do azdata BDC Spark](#azdata-bdc-spark-batch-create) | Crie um novo lote do Spark.
[lista de lotes do Spark no azdata BDC](#azdata-bdc-spark-batch-list) | Listar todos os lotes no Spark.
[informações do lote do azdata BDC Spark](#azdata-bdc-spark-batch-info) | Obtenha informações sobre um lote do Spark ativo.
[log do lote do azdata BDC Spark](#azdata-bdc-spark-batch-log) | Obter logs de execução para um lote do Spark.
[Estado de lote do azdata BDC Spark](#azdata-bdc-spark-batch-state) | Obter estado de execução para um lote do Spark.
[exclusão em lote do azdata BDC Spark](#azdata-bdc-spark-batch-delete) | Excluir um lote do Spark.
## <a name="azdata-bdc-spark-batch-create"></a>criação de lote do azdata BDC Spark
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
Crie um novo lote do Spark.
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--file -f`
Caminho para o arquivo a ser executado.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--class-name -c`
Nome da classe a ser executada ao passar um ou mais arquivos jar.
#### `--arguments -a`
Lista de argumentos.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--jar-files -j`
Lista de caminhos de arquivo jar.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--py-files -p`
Lista de caminhos de arquivo do Python.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--files`
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
#### `--archives`
Lista de caminhos de arquivos mortos.  Para passar uma lista JSON codifique os valores.  Exemplo: ' ["entry1", "entry2"] '.
#### `--queue -q`
Nome da fila do Spark na qual executar a sessão.
#### `--name -n`
Nome da sessão do Spark.
#### `--config`
Lista de pares de valor de nome que contêm valores de configuração do Spark.  Codificado como dicionário JSON.  Exemplo: ' {"Name": "value", "nome2": "value2"} '.
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
## <a name="azdata-bdc-spark-batch-list"></a>lista de lotes do Spark no azdata BDC
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
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-spark-batch-info"></a>informações do lote do azdata BDC Spark
Isso obtém as informações de um lote do Spark com a ID fornecida.  A ID do lote é retornada de ' Spark batch Create '.
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>Exemplos
Obter informações do lote para o lote com a ID 0.
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--batch-id -i`
Número de ID do lote do Spark.
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
## <a name="azdata-bdc-spark-batch-log"></a>log do lote do azdata BDC Spark
Isso obtém as entradas de log do lote para um lote do Spark com a ID fornecida.  A ID do lote é retornada de ' Spark batch Create '.
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>Exemplos
Obtenha o log do lote para o lote com a ID 0.
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--batch-id -i`
Número de ID do lote do Spark.
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
## <a name="azdata-bdc-spark-batch-state"></a>Estado de lote do azdata BDC Spark
Isso Obtém o estado do lote para um lote do Spark com a ID fornecida.  A ID do lote é retornada de ' Spark batch Create '.
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>Exemplos
Obter o estado do lote para o lote com a ID 0.
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--batch-id -i`
Número de ID do lote do Spark.
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
## <a name="azdata-bdc-spark-batch-delete"></a>exclusão em lote do azdata BDC Spark
Isso exclui um lote do Spark. A ID do lote é retornada de ' Spark batch Create '.
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>Exemplos
Excluir um lote.
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--batch-id -i`
Número de ID do lote do Spark.
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
