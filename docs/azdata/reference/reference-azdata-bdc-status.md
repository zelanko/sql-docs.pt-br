---
title: azdata bdc status reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc status de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 536e9b87cd6c6477b235746a792f3585e4f3259d
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358354"
---
# <a name="azdata-bdc-status"></a>azdata bdc status

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata bdc status show](#azdata-bdc-status-show) | Mostra o status atual do BDC.
## <a name="azdata-bdc-status-show"></a>azdata bdc status show
Mostra o status atual do BDC.
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).

