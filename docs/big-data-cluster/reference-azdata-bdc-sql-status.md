---
title: azdata bdc sql status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata bdc sql status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 81c1a84ea196e7f986f9427605de575f59a3152c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531707"
---
# <a name="azdata-bdc-sql-status"></a>azdata bdc sql status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[azdata bdc sql status show](#azdata-bdc-sql-status-show) | Status do serviço Sql-server.
## <a name="azdata-bdc-sql-status-show"></a>azdata bdc sql status show
Status do serviço Sql-server.
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>Exemplos
Obter o status do serviço sql.
```bash
azdata bdc sql status show
```
Obter o status do serviço sql com todas as instâncias.
```bash
azdata bdc sql status show --all
```
Obter o status do recurso mestre no serviço sql.
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
