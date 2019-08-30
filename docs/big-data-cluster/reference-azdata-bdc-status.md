---
title: azdata bdc status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc status de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 712a5ac51f13450fe5cf6b8cc13400d5666eb4a0
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155202"
---
# <a name="azdata-bdc-status"></a>azdata bdc status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc status show](#azdata-bdc-status-show) | Mostra o status do BDC.
## <a name="azdata-bdc-status-show"></a>azdata bdc status show
Mostra o status do BDC.
```bash
azdata bdc status show [--resource -r] 
                       [--all -a]
```
### <a name="examples"></a>Exemplos
Status do BDC a que o usuário está conectado.
```bash
azdata bdc status show
```
Status do BDC com todas as instâncias dos recursos incluídos.
```bash
azdata bdc status show --all
```
Status do BDC dos serviços que incluem o recurso de controle.
```bash
azdata bdc status show --resource control
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--resource -r`
Obter os serviços associados a este recurso.
#### `--all -a`
Mostrar todas as instâncias de cada recurso dentro dos serviços.
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
