---
title: Referência do azdata arc dc status
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc dc status.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 82408e8a7f1edb37c33a6f1748119f5ff24f563f
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942264"
---
# <a name="azdata-arc-dc-status"></a>azdata arc dc status

Aplica-se ao `azdata`

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc dc status show](#azdata-arc-dc-status-show) | Mostra o status do controlador de dados.
## <a name="azdata-arc-dc-status-show"></a>azdata arc dc status show
Mostra o status do controlador de dados.
```bash
azdata arc dc status show [--namespace -ns] 
                          
```
### <a name="examples"></a>Exemplos
Mostra o status do controlador de dados em um namespace específico.
```bash
azdata arc dc status show --namespace <ns>
```
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--namespace -ns`
O namespace do Kubernetes no qual o controlador de dados existe.
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

