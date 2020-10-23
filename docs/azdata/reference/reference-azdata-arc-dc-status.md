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
ms.openlocfilehash: 817571e809ab9ea4133a2f1933c3b23d99d9b1bc
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358784"
---
# <a name="azdata-arc-dc-status"></a>azdata arc dc status

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

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

