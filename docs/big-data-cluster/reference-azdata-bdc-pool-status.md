---
title: referência de status do pool BDC azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de status do pool do azdata BDC.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0a5925af4f16f2147988b2318880d9acec664c3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426126"
---
# <a name="azdata-bdc-pool-status"></a>status do pool BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **status do pool do BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Mostrar status do pool BDC do azdata](#azdata-bdc-pool-status-show) | Status do pool.
## <a name="azdata-bdc-pool-status-show"></a>Mostrar status do pool BDC do azdata
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
Obtenha o status do pool mestre.
```bash
azdata bdc pool status show --kind master --name default
```
Obtenha o status do pool do Spark.
```bash
azdata bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--kind -k`
Tipo de pool de cluster de Big Data.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do pool de cluster de Big Data.
`default`
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

Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).
