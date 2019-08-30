---
title: azdata bdc pool status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc pool status de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ee49ee09107c98047bd5aea849b9ae486eb6736a
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153108"
---
# <a name="azdata-bdc-pool-status"></a>azdata bdc pool status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc pool status show](#azdata-bdc-pool-status-show) | Status do pool.
## <a name="azdata-bdc-pool-status-show"></a>azdata bdc pool status show
Status do pool.
```bash
azdata bdc pool status show --kind -k 
                            [--name -n]
```
### <a name="examples"></a>Exemplos
Obter o status do pool de armazenamento.
```bash
azdata bdc pool status show --kind storage --name default
```
Obter o status do pool de dados.
```bash
azdata bdc pool status show --kind data --name default
```
Obter o status do pool de computação.
```bash
azdata bdc pool status show --kind compute --name default
```
Obter o status do pool mestre.
```bash
azdata bdc pool status show --kind master --name default
```
Obter o status do pool do Spark.
```bash
azdata bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--kind -k`
Tipo de pool do cluster de Big Data.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do pool do cluster de Big Data.
`default`
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
