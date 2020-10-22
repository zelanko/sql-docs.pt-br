---
title: azdata bdc app status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata bdc app status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1b67f5bff93afc23cfecfb88c115cc55bf38df9a
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358644"
---
# <a name="azdata-bdc-app-status"></a>azdata bdc app status

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
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

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para saber mais sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).

