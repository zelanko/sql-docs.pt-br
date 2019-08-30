---
title: referência de status do azdata BDC Spark
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de status do azdata BDC Spark.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 96d2bf17e051f45a3041a911cce71c42827768d8
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158061"
---
# <a name="azdata-bdc-spark-status"></a>status do Spark do azdata BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Mostrar status do azdata BDC Spark](#azdata-bdc-spark-status-show) | Status do serviço Spark.
## <a name="azdata-bdc-spark-status-show"></a>Mostrar status do azdata BDC Spark
Status do serviço Spark.
```bash
azdata bdc spark status show [--resource -r] 
                             [--all -a]
```
### <a name="examples"></a>Exemplos
Obter o status do serviço Spark.
```bash
azdata bdc spark status show
```
Obter o status do serviço Spark com todas as instâncias.
```bash
azdata bdc spark status show --all
```
Obtenha o status do recurso de armazenamento no serviço Spark.
```bash
azdata bdc spark status show --resource storage-0
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--resource -r`
Obter este recurso neste serviço.
#### `--all -a`
Mostrar todas as instâncias de cada recurso dentro do serviço.
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

- Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

- Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
