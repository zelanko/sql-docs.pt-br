---
title: referência de cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para os comandos de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c69aeced2378e018376172e1fb6370d56706ecb7
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775642"
---
# <a name="mssqlctl-cluster"></a>Cluster do mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[Criar cluster mssqlctl](#mssqlctl-cluster-create) | Crie o cluster.
[exclusão de cluster mssqlctl](#mssqlctl-cluster-delete) | Exclua o cluster.
[configuração de cluster mssqlctl](reference-mssqlctl-cluster-config.md) | Comandos de configuração do cluster.
[depuração de cluster mssqlctl](reference-mssqlctl-cluster-debug.md) | Comandos de depuração.
## <a name="mssqlctl-cluster-create"></a>Criar cluster mssqlctl
Crie um Cluster de Big Data do SQL Server.
```bash
mssqlctl cluster create [--config-file -f] 
                        [--accept-eula -e]  
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-file -f`
Perfil de configuração, usado para implantar o cluster do cluster: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
#### `--accept-eula -e`
Você aceita os termos de licença? [Sim/não].
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
## <a name="mssqlctl-cluster-delete"></a>exclusão de cluster mssqlctl
Exclua o Cluster de Big Data do SQL Server.
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do cluster, usado para o namespace de kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--force -f`
Cluster de exclusão de força.
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
