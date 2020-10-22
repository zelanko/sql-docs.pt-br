---
title: Referência do azdata arc resource-kind
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc resource-kind.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 68d6d4c30e43804c8c18a7dc36d0a9d53bcb5677
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358704"
---
# <a name="azdata-arc-resource-kind"></a>azdata arc resource-kind

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc resource-kind list](#azdata-arc-resource-kind-list) | Lista os tipos de recursos personalizados disponíveis para o Arc que podem ser definidos e criados.
[azdata arc resource-kind get](#azdata-arc-resource-kind-get) | Obtém o arquivo de modelo do tipo de recurso do Arc.
## <a name="azdata-arc-resource-kind-list"></a>azdata arc resource-kind list
Lista os tipos de recursos personalizados disponíveis para o Arc que podem ser definidos e criados. Após a listagem, é possível continuar a obter o arquivo de modelo necessário para definir ou criar esse recurso personalizado.
```bash
azdata arc resource-kind list 
```
### <a name="examples"></a>Exemplos
Exemplo de comando para listar os tipos de recursos personalizados disponíveis para o Arc.
```bash
azdata arc resource-kind list
```
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
## <a name="azdata-arc-resource-kind-get"></a>azdata arc resource-kind get
Obtém o arquivo de modelo do tipo de recurso do Arc.
```bash
azdata arc resource-kind get --kind -k 
                             [--dest -d]
```
### <a name="examples"></a>Exemplos
Exemplo de comando para obter um arquivo de modelo CRD de um tipo de recurso do Arc.
```bash
azdata arc resource-kind get --kind sqldb
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--kind -k`
O tipo de recurso do Arc para o qual você deseja o arquivo de modelo.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--dest -d`
O diretório em que você deseja colocar os arquivos de modelo.
`template`
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

