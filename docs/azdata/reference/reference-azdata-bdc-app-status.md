---
title: azdata bdc app status reference
titleSuffix: SQL Server big data clusters
description: Use este artigo de referência para entender os comandos SQL na ferramenta azdata, especificamente o comando bdc app status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fd6288649db641bc846b8ebed3b997aa0092d36e
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733472"
---
# <a name="azdata-bdc-app-status"></a>azdata bdc app status

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descrição |
| --- | --- |
[azdata bdc app status show](#azdata-bdc-app-status-show) | Status do serviço de aplicativo.
## <a name="azdata-bdc-app-status-show"></a>azdata bdc app status show
Status do serviço de aplicativo.
```bash
azdata bdc app status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>Exemplos
Obter o status do serviço de aplicativo.
```bash
azdata bdc app status show
```
Obter o status do serviço de aplicativo com todas as instâncias.
```bash
azdata bdc app status show --all
```
Obter o status do recurso appproxy no serviço de aplicativo.
```bash
azdata bdc app status show --resource appproxy
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](../install/deploy-install-azdata.md).
