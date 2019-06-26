---
title: mssqlctl bdc config reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de bdc mssqlctl.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f57ba87ea7cbd770380497bd340b5eaa4d80f29c
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394158"
---
# <a name="mssqlctl-bdc-config"></a>configuração do bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **config bdc** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[mssqlctl bdc config show](#mssqlctl-bdc-config-show) | Obtém o Big Data da configuração do Cluster atual.
[mssqlctl bdc config init](#mssqlctl-bdc-config-init) | Inicializa um Cluster grande de dados criar perfil de configuração que pode ser usado com o cluster.
[lista de configuração do bdc mssqlctl](#mssqlctl-bdc-config-list) | Lista as opções de perfil de configuração disponíveis.
[seção de configuração do bdc mssqlctl](reference-mssqlctl-bdc-config-section.md) | Comandos para trabalhar com as seções individuais do perfil de configuração do Cluster de Big Data.
## <a name="mssqlctl-bdc-config-show"></a>mssqlctl bdc config show
Obtém o perfil de configuração atual do Cluster de dados grande e envia para o diretório de destino ou bastante o imprime no console.
```bash
mssqlctl bdc config show [--target -t] 
                         [--force -f]
```
### <a name="examples"></a>Exemplos
Mostrar a configuração do BDC em seu console
```bash
mssqlctl bdc config show
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
## <a name="mssqlctl-bdc-config-init"></a>mssqlctl bdc config init
Inicializa um Cluster grande de dados criar perfil de configuração que pode ser usado com o cluster. A fonte específica do perfil de configuração pode ser especificada nos argumentos de 3 opções.
```bash
mssqlctl bdc config init [--target -t] 
                         [--source -s]  
                         [--force -f]
```
### <a name="examples"></a>Exemplos
Experiência de init interativa do config BDC - você receberá prompts para os valores necessários.
```bash
mssqlctl bdc config init
```
Inicialização de configuração do BDC com argumentos, cria um perfil de configuração do aks – desenvolvimento / teste no. / personalizados.
```bash
mssqlctl bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Caminho do arquivo de onde você deseja que o perfil de config colocado, o padrão é cwd com personalizado-config. JSON.
#### `--source -s`
Config profile source: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
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
## <a name="mssqlctl-bdc-config-list"></a>lista de configuração do bdc mssqlctl
Lista opções de perfil de configuração disponíveis para uso em `bdc config init`
```bash
mssqlctl bdc config list [--config-profile -c] 
                         
```
### <a name="examples"></a>Exemplos
Mostra todos os nomes de perfil de configuração disponíveis.
```bash
mssqlctl bdc config list
```
Mostra o json de um perfil de configuração específica.
```bash
mssqlctl bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-profile -c`
Default config profile: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
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