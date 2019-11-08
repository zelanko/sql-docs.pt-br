---
title: azdata bdc endpoint reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc endpoint de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f5f5c25def3408d9b8ed396536e34cc9b247a7a
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531824"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[azdata bdc endpoint list](#azdata-bdc-endpoint-list) | Lista os pontos de extremidade para o cluster de Big Data.
## <a name="azdata-bdc-endpoint-list"></a>azdata bdc endpoint list
Lista os pontos de extremidade para o cluster de Big Data.
```bash
azdata bdc endpoint list [--endpoint-name -e] 
       ```
### Optional Parameters
#### `--endpoint-name -e`
Big data cluster endpoint name.
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org/) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.

## Next steps

For more information about other `azdata` commands, see [azdata reference](reference-azdata.md). For more information about how to install the `azdata` tool, see [Install azdata to manage SQL Server 2019 big data clusters](deploy-install-azdata.md).
