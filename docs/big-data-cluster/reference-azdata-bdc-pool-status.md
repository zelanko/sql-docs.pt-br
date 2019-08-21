---
title: azdata bdc pool status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc pool status de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eafc72c6d86d38eabd26b735a9d5dab967e2e6be
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653488"
---
# <a name="azdata-bdc-pool-status"></a>azdata bdc pool status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos **bdc pool status** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md).

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

Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]gerenciar ](deploy-install-azdata.md).
