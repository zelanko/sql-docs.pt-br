---
title: referência de instrução do azdata BDC Spark
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de instrução do azdata BDC Spark.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 778980ac6b93e7db79d59182fbd18ab4cfdb8b75
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426086"
---
# <a name="azdata-bdc-spark-statement"></a>instrução azdata BDC Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

O artigo a seguir fornece referência para os comandos de **instrução do BDC Spark** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[lista de instruções do azdata BDC Spark](#azdata-bdc-spark-statement-list) | Listar todas as instruções na sessão do Spark fornecida.
[criação da instrução do azdata BDC Spark](#azdata-bdc-spark-statement-create) | Crie uma nova instrução do Spark na sessão especificada.
[informações da instrução do azdata BDC Spark](#azdata-bdc-spark-statement-info) | Obtenha informações sobre a instrução solicitada na sessão do Spark fornecida.
[cancelamento da instrução do azdata BDC Spark](#azdata-bdc-spark-statement-cancel) | Cancele uma instrução dentro da sessão do Spark fornecida.
## <a name="azdata-bdc-spark-statement-list"></a>lista de instruções do azdata BDC Spark
Listar todas as instruções na sessão do Spark fornecida.
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>Exemplos
Listar todas as instruções de sessão.
```bash
azdata spark statement list --session-id 0
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
## <a name="azdata-bdc-spark-statement-create"></a>criação da instrução do azdata BDC Spark
Isso cria e executa uma nova instrução na sessão especificada.  Se a execução for rápida, o resultado conterá a saída da execução.  Caso contrário, o resultado poderá ser recuperado usando ' informações de sessão do Spark ' depois que a instrução for concluída.
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>Exemplos
Execute uma instrução.
```bash
azdata spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
#### `--code -c`
Cadeia de caracteres que contém o código a ser executado como parte da instrução.
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
## <a name="azdata-bdc-spark-statement-info"></a>informações da instrução do azdata BDC Spark
Isso Obtém o status de execução e os resultados da execução se a instrução for concluída. A ID da instrução é retornada de ' Spark Statement Create '.
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>Exemplos
Obter informações de instrução para a sessão com ID 0 e ID de instrução 0.
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
#### `--statement-id -s`
Número de ID da instrução do Spark dentro da ID de sessão fornecida.
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
## <a name="azdata-bdc-spark-statement-cancel"></a>cancelamento da instrução do azdata BDC Spark
Isso cancela uma instrução dentro da sessão do Spark fornecida. A ID da instrução é retornada de ' Spark Statement Create '.
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>Exemplos
Cancelar uma instrução.
```bash
azdata spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--session-id -i`
Número de ID da sessão do Spark.
#### `--statement-id -s`
Número de ID da instrução do Spark dentro da ID de sessão fornecida.
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
