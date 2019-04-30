---
title: referência de modelo de aplicativo mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de modelo de aplicativo mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0b4cbae0ba35c0cef777b3535b2012ab78f8e6da
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473445"
---
# <a name="mssqlctl-app-template"></a>Modelo de aplicativo do mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **modelo de aplicativo** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[lista de modelos de aplicativo mssqlctl](#mssqlctl-app-template-list) | Modelos de Fetch com suporte.
[mssqlctl pull de modelo de aplicativo](#mssqlctl-app-template-pull) | Baixe os modelos com suporte.
## <a name="mssqlctl-app-template-list"></a>lista de modelos de aplicativo mssqlctl
Modelos de Fetch com suporte no repositório do github [URL] especificado.
```bash
mssqlctl app template list [--url -u] 
                           
```
### <a name="examples"></a>Exemplos
Busca todos os modelos em um local de repositório do modelo padrão.
```bash
mssqlctl app template list
```
Busca todos os modelos em um local de repositório diferente.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--url -u`
Especifique um local de repositório de modelo diferente. Padrão: https://github.com/Microsoft/SQLBDC-AppDeploy.git
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.
## <a name="mssqlctl-app-template-pull"></a>mssqlctl pull de modelo de aplicativo
Baixe os modelos com suporte no repositório do github [URL] especificado.
```bash
mssqlctl app template pull [--name -n] 
                           [--url -u]  
                           [--destination -d]
```
### <a name="examples"></a>Exemplos
Baixe todos os modelos em um local de repositório do modelo padrão.
```bash
mssqlctl app template pull
```
Baixe todos os modelos em um local de repositório diferente.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
Baixe o modelo individual por nome.
```bash
mssqlctl app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do modelo. Para obter uma lista completa off namesrun modelo com suporte `mssqlctl app template list`
#### `--url -u`
Especifique um local de repositório de modelo diferente. Padrão: https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Onde colocar o modelo de aplicativo de esqueleto.
`./templates`
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o nível de detalhes de registro em log para mostrar que todos os logs de depuração.
#### `--help -h`
Mostre esta mensagem de Ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Ver [ http://jmespath.org/ ](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumente o nível de detalhes do registro em log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).