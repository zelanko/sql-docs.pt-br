---
title: referência de configuração de cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para os comandos de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 74097057702ad32a803c440d92b0ed7c8f855880
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779421"
---
# <a name="mssqlctl-cluster-config"></a>Configuração de cluster do mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **configuração do cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[mssqlctl show de configuração de cluster](#mssqlctl-cluster-config-show) | Obtém a configuração atual do SQL Server Big Data do Cluster.
[inicialização de configuração de cluster mssqlctl](#mssqlctl-cluster-config-init) | Inicializa um perfil de configuração de cluster que pode ser usado com o cluster crie.
[lista de configuração de cluster mssqlctl](#mssqlctl-cluster-config-list) | Lista as opções de arquivo de configuração disponíveis.
[seção de configuração de cluster mssqlctl](reference-mssqlctl-cluster-config-section.md) | Comandos para trabalhar com as seções individuais do arquivo de configuração de cluster.
## <a name="mssqlctl-cluster-config-show"></a>mssqlctl show de configuração de cluster
Obtém o arquivo de configuração atual do SQL Server Big Data do Cluster e o envia para o arquivo de destino ou bastante o imprime no console.
```bash
mssqlctl cluster config show [--target -t] 
                             [--force -f]
```
### <a name="examples"></a>Exemplos
Mostrar a configuração de cluster no console do
```bash
mssqlctl cluster config show
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Arquivo de saída para armazenar o resultado no. Padrão: direcionado para stdout.
#### `--force -f`
Força a substituição do arquivo de destino.
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
Inicializa um perfil de configuração de cluster que pode ser usado com o cluster crie. A fonte específica do perfil de configuração pode ser especificada nos argumentos de 3 opções.
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]  
                             [--force -f]
```
### <a name="examples"></a>Exemplos
Experiência de inicialização do cluster config - orientada receberá prompts para os valores necessários.
```bash
mssqlctl cluster config init
```
Init config com argumentos de cluster, cria um perfil de configuração do aks-dev-test,. / custom.json.
```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Caminho do arquivo de onde você deseja que o perfil de config colocado, o padrão é cwd com personalizado-config. JSON.
#### `--src -s`
Config profile source: ['aks-dev-test.json', 'kubeadm-dev-test.json', 'minikube-dev-test.json']
#### `--force -f`
Força a substituição do arquivo de destino.
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
mssqlctl cluster config list [--config-file -c] 
                             
```
### <a name="examples"></a>Exemplos
Mostra todos os nomes de perfil de configuração disponíveis.
```bash
mssqlctl cluster config list
```
Mostra o json de um perfil de configuração específica.
```bash
mssqlctl cluster config list --config-file aks-dev-test.json
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-file -c`
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