---
title: referência de modelo de aplicativo azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de modelo de aplicativo azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3b257a2bacc56a7907ab0d25f492ed0ebd605543
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426326"
---
# <a name="azdata-app-template"></a>modelo de aplicativo azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **modelo de aplicativo** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[lista de modelos de aplicativo azdata](#azdata-app-template-list) | Buscar modelos com suporte.
[pull de modelo de aplicativo azdata](#azdata-app-template-pull) | Baixar modelos com suporte.
## <a name="azdata-app-template-list"></a>lista de modelos de aplicativo azdata
Busque os modelos com suporte no repositório GitHub [URL] especificado.
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>Exemplos
Busque todos os modelos no local do repositório de modelos padrão.
```bash
azdata app template list
```
Busque todos os modelos em um local de repositório diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--url -u`
Especifique um local de repositório de modelos diferente. Os https://github.com/Microsoft/SQLBDC-AppDeploy.git
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-app-template-pull"></a>pull de modelo de aplicativo azdata
Baixe os modelos com suporte no repositório GitHub [URL] especificado.
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         [--destination -d]
```
### <a name="examples"></a>Exemplos
Baixe todos os modelos no local do repositório de modelos padrão.
```bash
azdata app template pull
```
Baixe todos os modelos em um local de repositório diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
Baixar modelo individual por nome.
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do modelo. Para obter uma lista completa de modelos com suporte namesrun`azdata app template list`
#### `--url -u`
Especifique um local de repositório de modelos diferente. Os https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Onde posicionar o modelo de esqueleto do aplicativo.
`./templates`
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).
