---
title: referência de bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de bdc mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2c16a8121f2a0ec90fe8141c78e690bf212b5f27
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394228"
---
# <a name="mssqlctl-bdc"></a>mssqlctl bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **bdc** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[Criar mssqlctl bdc](#mssqlctl-bdc-create) | Crie um Cluster de Big Data.
[mssqlctl bdc delete](#mssqlctl-bdc-delete) | Exclua o Cluster de Big Data.
[mssqlctl bdc config](reference-mssqlctl-bdc-config.md) | Comandos de configuração.
[o ponto de extremidade do mssqlctl bdc](reference-mssqlctl-bdc-endpoint.md) | Comandos de ponto de extremidade.
[status do bdc mssqlctl](reference-mssqlctl-bdc-status.md) | Comandos de status.
[depuração de bdc mssqlctl](reference-mssqlctl-bdc-debug.md) | Comandos de depuração.
[pool de armazenamento do bdc mssqlctl](reference-mssqlctl-bdc-storage-pool.md) | Comandos de pool de armazenamento.
[controle de bdc mssqlctl](reference-mssqlctl-bdc-control.md) | Comandos de controle.
[pool de bdc mssqlctl](reference-mssqlctl-bdc-pool.md) | Comandos de pool.
## <a name="mssqlctl-bdc-create"></a>Criar mssqlctl bdc
Criar um Cluster grande de dados do SQL Server - configuração do kube é necessária no seu sistema, juntamente com as seguintes variáveis de ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'DOCKER_USERNAME', 'DOCKER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'].
```bash
mssqlctl bdc create [--config-profile -c] 
                    [--accept-eula -a]  
                    [--node-label -l]  
                    [--force -f]
```
### <a name="examples"></a>Exemplos
Experiência de implantação do BDC guiada - você receberá prompts para os valores necessários.
```bash
mssqlctl bdc create
```
Implantação do BDC com argumentos.
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test
```
Implantação do BDC com argumentos - nenhum aviso será dado como--force sinalizador é usado.
```bash
mssqlctl bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-profile -c`
Perfil de configuração BDC, usado para implantar o cluster: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--accept-eula -a`
Você aceita os termos de licença? [Sim/não]. Se você não quiser usar esse arg, você pode definir a variável de ambiente ACCEPT_EULA como 'Sim'
#### `--node-label -l`
Rótulo do nó BDC, usado para designar quais nós para implantar.
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
## <a name="mssqlctl-bdc-delete"></a>exclusão de bdc mssqlctl
Excluir o Cluster grande de dados do SQL Server - configuração do kube é necessária no seu sistema, juntamente com as seguintes variáveis de ambiente ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'].
```bash
mssqlctl bdc delete --name -n 
                    [--force -f]
```
### <a name="examples"></a>Exemplos
Exclusão de BDC em que o controlador username e password já estão definidos no seu ambiente de sistema.
```bash
mssqlctl bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do BDC, usado para o namespace de kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--force -f`
Forçar Exclusão BDC.
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
