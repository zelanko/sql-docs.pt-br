---
title: azdata context reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de contexto.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f2716a8176124539aa7caf382193359ff5435aa6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820997"
---
# <a name="azdata-context"></a>azdata context

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `context` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata context list](#azdata-context-list) | Lista os contextos disponíveis no perfil do usuário.
[azdata context delete](#azdata-context-delete) | Exclui o contexto com o namespace fornecido do perfil do usuário.
[azdata context set](#azdata-context-set) | Define o contexto com o namespace fornecido como o contexto ativo no perfil do usuário.
## <a name="azdata-context-list"></a>azdata context list
Você pode definir ou excluir qualquer um deles com `azdata context set` ou `azdata context delete`. Para fazer logon em um novo contexto, use `azdata login`.
```bash
azdata context list [--active -a] 
  ```
### <a name="examples"></a>Exemplos
Lista todos os contextos disponíveis no perfil do usuário.
```bash
azdata context list
```
Lista o contexto ativo no perfil do usuário.
```bash
azdata context list --active
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--active -a`
Lista somente o contexto ativo no momento.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-context-delete"></a>azdata context delete
Se o contexto excluído estiver ativo, o usuário precisará definir um novo contexto ativo. Para ver contextos disponíveis para definir ou excluir `azdata context list`
```bash
azdata context delete --namespace -n 
    ```
### Examples
Deletes contextNamespace from the user profile.
```bash
azdata context delete -n contextNamespace
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--namespace -n`
Namespace do contexto que você gostaria de excluir.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-context-set"></a>azdata context set
Para ver contextos disponíveis para definir `azdata context list`. Se nenhum contexto estiver listado, você precisará fazer logon para criar um contexto em seu perfil do usuário `azdata login`. Aquilo em que você fizer logon será o seu contexto ativo. Se você fizer logon em várias entidades, poderá alternar entre os contextos ativos com este comando. Para ver seu contexto ativo no momento `azdata context list --active`
```bash
azdata context set --namespace -n 
 ```
### <a name="examples"></a>Exemplos
Define contextNamespace como o contexto ativo no perfil do usuário.
```bash
azdata context set -n contextNamespace
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--namespace -n`
Namespace do contexto que você gostaria de definir.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
