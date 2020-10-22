---
title: azdata bdc gateway status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata bdc gateway status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f92ab04058d681af45bf2c6739dbfa582b27aa76
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358564"
---
# <a name="azdata-bdc-gateway-status"></a>azdata bdc gateway status

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata bdc gateway status show](#azdata-bdc-gateway-status-show) | Status do serviço de gateway.
## <a name="azdata-bdc-gateway-status-show"></a>azdata bdc gateway status show
Status do serviço de gateway.
```bash
azdata bdc gateway status show [--resource -r] 
                               [--all -a]
```
### <a name="examples"></a>Exemplos
Obter status do serviço de gateway.
```bash
azdata bdc gateway status show
```
Obter o status do serviço de gateway com todas as instâncias.
```bash
azdata bdc gateway status show --all
```
Obter o status do recurso de gateway no serviço de gateway.
```bash
azdata bdc gateway status show --resource gateway
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

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).

