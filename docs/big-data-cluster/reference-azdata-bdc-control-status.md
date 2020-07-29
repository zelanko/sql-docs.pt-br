---
title: azdata bdc control status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc control status de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5036e7646a847edfa38998694ace8b35d649dd5e
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942899"
---
# <a name="azdata-bdc-control-status"></a>azdata bdc control status

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
| Comando | Descrição |
| --- | --- |
[azdata bdc control status show](#azdata-bdc-control-status-show) | Status do serviço de controle.
## <a name="azdata-bdc-control-status-show"></a>azdata bdc control status show
Status do serviço de controle.
```bash
azdata bdc control status show [--resource -r] 
                               [--all -a]
```
### <a name="examples"></a>Exemplos
Obter o status do serviço.
```bash
azdata bdc control status show
```
Obter o status do serviço de controle com todas as instâncias.
```bash
azdata bdc control status show --all
```
Obter o status do recurso de controle dentro do serviço de controle.
```bash
azdata bdc control status show --resource control
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

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
