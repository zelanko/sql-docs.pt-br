---
title: azdata bdc spark statement reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc spark statement de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 57044b75219f4c2827c322c100a5d25d5f0b274a
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653191"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark statement

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

O artigo a seguir fornece referência para os comandos **bdc spark statement** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc spark statement list](#azdata-bdc-spark-statement-list) | Listar todas as instruções na sessão do Spark fornecida.
[azdata bdc spark statement create](#azdata-bdc-spark-statement-create) | Criar uma nova instrução do Spark na sessão especificada.
[azdata bdc spark statement info](#azdata-bdc-spark-statement-info) | Obter informações sobre a instrução solicitada na sessão do Spark fornecida.
[azdata bdc spark statement cancel](#azdata-bdc-spark-statement-cancel) | Cancelar uma instrução dentro da sessão do Spark fornecida.
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark statement list
Listar todas as instruções na sessão do Spark fornecida.
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>Exemplos
Listar todas as instruções da sessão.
```bash
azdata bdc spark statement list --session-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark statement create
Isso cria e executa uma nova instrução na sessão especificada.  Se a execução for rápida, o resultado conterá a saída da execução.  Caso contrário, o resultado poderá ser recuperado usando 'spark session info' depois que a instrução for concluída.
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>Exemplos
Executar uma instrução.
```bash
azdata bdc spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
#### `--code -c`
Cadeia de caracteres que contém código a ser executado como parte da instrução.
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
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark statement info
Isso obtém o status de execução e os resultados da execução se a instrução for concluída. A ID da instrução é retornada de 'spark statement create'.
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>Exemplos
Obter informações de instrução para a sessão com a ID 0 e a ID de instrução 0.
```bash
azdata bdc spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
#### `--statement-id -s`
Número de ID da instrução do Spark dentro da ID de sessão fornecida.
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
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark statement cancel
Isso cancela uma instrução dentro da sessão do Spark fornecida. A ID da instrução é retornada de 'spark statement create'.
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>Exemplos
Cancelar uma instrução.
```bash
azdata bdc spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
#### `--statement-id -s`
Número de ID da instrução do Spark dentro da ID de sessão fornecida.
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

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]gerenciar ](deploy-install-azdata.md).
