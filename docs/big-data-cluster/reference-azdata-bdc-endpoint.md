---
title: referência do ponto de extremidade do BDC azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de ponto de extremidade do azdata BDC.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: db24ca1ca1bb6fa25ddd7486fe041ea54722276c
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426206"
---
# <a name="azdata-bdc-endpoint"></a>ponto de extremidade do BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **ponto de extremidade do BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[lista de pontos de extremidade do BDC azdata](#azdata-bdc-endpoint-list) | Lista os pontos de extremidade para o cluster de Big Data.
## <a name="azdata-bdc-endpoint-list"></a>lista de pontos de extremidade do BDC azdata
Lista os pontos de extremidade para o cluster de Big Data.
```bash
azdata bdc endpoint list [--endpoint-name -e] 
                         
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--endpoint-name -e`
Nome do ponto de extremidade do cluster de Big Data.
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
