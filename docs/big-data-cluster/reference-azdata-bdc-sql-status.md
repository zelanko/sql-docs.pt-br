---
title: referência de status do SQL do BDC do azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de status do SQL do azdata BDC.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c5c2cdd924f266400125080d21d0461d5f599190
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158251"
---
# <a name="azdata-bdc-sql-status"></a>status do SQL do azdata BDC

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Mostrar status do SQL do BDC do azdata](#azdata-bdc-sql-status-show) | Status do serviço SQL-Server.
## <a name="azdata-bdc-sql-status-show"></a>Mostrar status do SQL do BDC do azdata
Status do serviço SQL-Server.
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>Exemplos
Obter o status do serviço SQL.
```bash
azdata bdc sql status show
```
Obter o status do serviço SQL com todas as instâncias.
```bash
azdata bdc sql status show --all
```
Obter o status do recurso mestre no serviço SQL.
```bash
azdata bdc sql status show --resource master
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
