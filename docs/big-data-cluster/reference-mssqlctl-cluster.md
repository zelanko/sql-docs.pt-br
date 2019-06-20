---
title: referência de cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para os comandos de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 654888bc27fec43abb8a8f511b0de7a4972e4377
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779261"
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
[ponto de extremidade de cluster mssqlctl](reference-mssqlctl-cluster-endpoint.md) | Comandos de ponto de extremidade.
[status do cluster mssqlctl](reference-mssqlctl-cluster-status.md) | Comandos de status.
[depuração de cluster mssqlctl](reference-mssqlctl-cluster-debug.md) | Comandos de depuração.
[pool de armazenamento do cluster mssqlctl](reference-mssqlctl-cluster-storage-pool.md) | Gerencie pools de armazenamento do cluster.
## <a name="mssqlctl-cluster-create"></a>Criar cluster mssqlctl
Criar um Cluster grande de dados do SQL Server - configuração do kube é necessária no seu sistema, juntamente com as seguintes variáveis de ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'DOCKER_USERNAME', 'DOCKER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
mssqlctl cluster create [--config-file -c] 
                        [--accept-eula -a]  
                        [--node-label -l]  
                        [--force -f]
```
### <a name="examples"></a>Exemplos
Experiência de implantação de cluster - orientada receberá prompts para os valores necessários.
```bash
mssqlctl cluster create
```
Implantação de cluster com argumentos.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json
```
Implantação de cluster com argumentos - nenhum aviso será dado como--force sinalizador é usado.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json --force
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-file -c`
Perfil de configuração, usado para implantar o cluster do cluster: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
#### `--accept-eula -a`
Você aceita os termos de licença? [Sim/não]. Se você não quiser usar esse arg, você pode definir a variável de ambiente ACCEPT_EULA como 'Sim'
#### `--node-label -l`
Rótulo do nó, usado para designar quais nós implantar em um cluster.
#### `--force -f`
Criar Force, o usuário não será solicitado para todos os valores e todos os problemas serão impresso como parte de stderr.
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
Excluir o Cluster grande de dados do SQL Server - configuração do kube é necessária no seu sistema, juntamente com as seguintes variáveis de ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="examples"></a>Exemplos
Exclusão do cluster em que o controlador username e password já estão definidos no seu ambiente de sistema.
```bash
mssqlctl cluster delete --name <cluster_name>
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
