---
title: Referência do mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ebd3b63d641c77dae1afbff21264ec4fe34df4d0
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473463"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **mssqlctl** ferramenta para [clusters de big data de 2019 do SQL Server (visualização)](big-data-cluster-overview.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
|[aplicativo mssqlctl](reference-mssqlctl-app.md) | Criar, excluir, executar e gerenciar aplicativos. |
|[cluster mssqlctl](reference-mssqlctl-cluster.md) | Selecionar, gerenciar e operar clusters. |
[logon de mssqlctl](#mssqlctl-login) | Faça logon no cluster.
[mssqlctl logout](#mssqlctl-logout) | Faça logoff do cluster.
|[armazenamento mssqlctl](reference-mssqlctl-storage.md) | Gerencie o armazenamento de cluster. |
## <a name="mssqlctl-login"></a>logon de mssqlctl
Faça logon no cluster.
```bash
mssqlctl login [--username -u] 
               [--password -p]  
               [--endpoint -e]
```
### <a name="examples"></a>Exemplos
Faça logon interativamente.
```bash
mssqlctl login
```
Faça logon com nome de usuário e senha.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret
```
Faça logon com nome de usuário, senha e ponto de extremidade do cluster.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--username -u`
Conta do usuário.
#### `--password -p`
Credenciais de senha.
#### `--endpoint -e`
Cluster de host e a porta (ex) "http://host:port".
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
## <a name="mssqlctl-logout"></a>mssqlctl logout
Faça logoff do cluster.
```bash
mssqlctl logout 
```
### <a name="examples"></a>Exemplos
Fazer logoff deste usuário.
```bash
mssqlctl logout
```
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

Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).