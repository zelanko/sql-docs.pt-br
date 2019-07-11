---
title: referência de status do pool de bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de status de pool mssqlctl bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 818773708087927b5c2f3ccea44ba52cd77e7a71
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728563"
---
# <a name="mssqlctl-bdc-pool-status"></a>status do pool de bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **status do pool de bdc** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Mostrar de status de pool mssqlctl bdc](#mssqlctl-bdc-pool-status-show) | Status do pool.
## <a name="mssqlctl-bdc-pool-status-show"></a>Mostrar de status de pool mssqlctl bdc
Status do pool.
```bash
mssqlctl bdc pool status show --kind -k 
                              [--name -n]
```
### <a name="examples"></a>Exemplos
Obter o status do pool de armazenamento.
```bash
mssqlctl bdc pool status show --kind storage --name default
```
Obter o status do pool de dados.
```bash
mssqlctl bdc pool status show --kind data --name default
```
Obter o status do pool de computação.
```bash
mssqlctl bdc pool status show --kind compute --name default
```
Obter status do pool principal.
```bash
mssqlctl bdc pool status show --kind master --name default
```
Obter o status do pool do spark.
```bash
mssqlctl bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--kind -k`
Tipo de pool do BDC.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do pool BDC.
`default`
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).