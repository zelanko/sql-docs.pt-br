---
title: referência de configuração de cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para os comandos de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3a4693c5ffb68ad555d97d02f983fadf4e6bbd9a
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774673"
---
# <a name="mssqlctl-cluster-config"></a>Configuração de cluster do mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **configuração do cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[obter configuração de cluster mssqlctl](#mssqlctl-cluster-config-get) | Obter a configuração do cluster - kube configuração é necessária no seu sistema.
[inicialização de configuração de cluster mssqlctl](#mssqlctl-cluster-config-init) | Inicializa uma configuração de cluster.
[lista de configuração de cluster mssqlctl](#mssqlctl-cluster-config-list) | Lista as opções de arquivo de configuração disponíveis.
[seção de configuração de cluster mssqlctl](reference-mssqlctl-cluster-config-section.md) | Comandos para trabalhar com as seções individuais do arquivo de configuração.
## <a name="mssqlctl-cluster-config-get"></a>obter configuração de cluster mssqlctl
Obtém o arquivo de configuração atual do SQL Server Big Data do Cluster.
```bash
mssqlctl cluster config get --name -n 
                            [--output-file -f]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do cluster, usado para o namespace de kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--output-file -f`
Arquivo de saída para armazenar o resultado no. Padrão: direcionado para stdout.
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
## <a name="mssqlctl-cluster-config-init"></a>inicialização de configuração de cluster mssqlctl
Inicializa um arquivo de configuração de cluster para o usuário com base no tipo padrão especificado.
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Caminho do arquivo de onde você deseja que o arquivo de configuração colocado, o padrão é cwd com personalizado-config. JSON.
#### `--src -s`
Config source: ['aks-dev-test.json', 'kubeadm-dev-test.json', 'minikube-dev-test.json']
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
## <a name="mssqlctl-cluster-config-list"></a>lista de configuração de cluster mssqlctl
Lista as opções de arquivo de configuração disponíveis para uso na inicialização de configuração de cluster
```bash
mssqlctl cluster config list [--config-file -f] 
                             
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-file -f`
Default config file: ['aks-dev-test.json', 'kubeadm-dev-test.json', 'minikube-dev-test.json']
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