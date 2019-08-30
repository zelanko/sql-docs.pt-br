---
title: azdata app template reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata app template.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 07911616659a29df7f7fa6ce4d356a9c82789ae2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153226"
---
# <a name="azdata-app-template"></a>azdata app template

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata app template list](#azdata-app-template-list) | Buscar modelos com suporte.
[azdata app template pull](#azdata-app-template-pull) | Baixar modelos com suporte.
## <a name="azdata-app-template-list"></a>azdata app template list
Buscar modelos com suporte no repositório GitHub [URL] especificado.
```bash
azdata app template list 
```
### <a name="examples"></a>Exemplos
Buscar todos os modelos na localização do repositório de modelos padrão.
```bash
azdata app template list
```
Buscar todos os modelos em uma localização de repositório diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
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
## <a name="azdata-app-template-pull"></a>azdata app template pull
Baixar modelos com suporte no repositório GitHub [URL] especificado.
```bash
azdata app template pull 
```
### <a name="examples"></a>Exemplos
Baixar todos os modelos na localização do repositório de modelos padrão.
```bash
azdata app template pull
```
Baixar todos os modelos em uma localização de repositório diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
Baixar modelo individual por nome.
```bash
azdata app template pull --name ssis
```
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
