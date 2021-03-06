---
title: Referência do azdata arc postgres endpoint
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc postgres endpoint.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 097bfb40f8636f66f142fc785c4699dce2084440
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358754"
---
# <a name="azdata-arc-postgres-endpoint"></a>azdata arc postgres endpoint

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc postgres endpoint list](#azdata-arc-postgres-endpoint-list) | Liste pontos de extremidade de grupos de servidores PostgreSQL.
## <a name="azdata-arc-postgres-endpoint-list"></a>azdata arc postgres endpoint list
Liste pontos de extremidade de grupos de servidores PostgreSQL.
```bash
azdata arc postgres endpoint list --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>Exemplos
Liste pontos de extremidade de grupos de servidores PostgreSQL.
```bash
azdata arc postgres endpoint list -n postgres01
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
Nome do grupo de servidores PostgreSQL.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--engine-version -ev`
--engine-version pode ser usado em conjunto com --name para identificar um grupo de servidores de hiperescala do PostgreSQL quando dois grupos de servidores com versões de mecanismo diferentes têm o mesmo nome. --engine-version é opcional e, quando usado para identificar um grupo de servidores, deve ser igual a 11 ou 12.
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

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).

