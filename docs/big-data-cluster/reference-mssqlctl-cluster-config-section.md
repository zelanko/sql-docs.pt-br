---
title: referência de seção de configuração de cluster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de seção de configuração de cluster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5a793e7d0fcaf782a09a4981491ef0a8d90ab5a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759133"
---
# <a name="mssqlctl-cluster-config-section"></a>seção de configuração de cluster do mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **seção de configuração do cluster** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Commands
|     |     |
| --- | --- |
[seção de configuração de cluster mssqlctl obter](#mssqlctl-cluster-config-section-get) | Obtém uma seção de um arquivo de configuração.
[conjunto de seção de configuração de cluster mssqlctl](#mssqlctl-cluster-config-section-set) | Define uma seção para um arquivo de configuração.
## <a name="mssqlctl-cluster-config-section-get"></a>seção de configuração de cluster mssqlctl obter
Obtém a seção especificada do arquivo de configuração selecionado de acordo com o caminho json especificado.
```bash
mssqlctl cluster config section get --json-path -j 
                                    --config-file -f  
                                    [--target -t]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--json-path -j`
O caminho da chave json que leva para o valor desejado ou a seção do arquivo de configuração, ou seja, key1.key2.key3. Usa a linguagem de consulta jsonpath, https://github.com/h2non/jsonpath-ng, por exemplo: -j ' $. spec.pools [? ( @.spec.type = = "Mestre")]... pontos de extremidade
#### `--config-file -f`
Caminho do arquivo de configuração de cluster.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Caminho do arquivo de onde você deseja que o arquivo de seção colocado.
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
## <a name="mssqlctl-cluster-config-section-set"></a>conjunto de seção de configuração de cluster mssqlctl
Define a seção especificada no arquivo de configuração selecionado de acordo com o caminho json especificado.
```bash
mssqlctl cluster config section set --config-file -f 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -f`
Caminho do arquivo de configuração de cluster da configuração que você deseja definir para
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--json-values -j`
Uma lista de pares de valor de chave de caminhos de json para valores: key1.subkey1=value1,key2.subkey2=value2. Você pode fornecer embutido valores json, como: key ='{"tipo": "cluster", "name": "test-cluster"}' ou forneça um caminho de arquivo, como key=./values.json
#### `--patch-file -p`
Caminho para um arquivo json de patch que baseia-se a biblioteca jsonpatch e jsonpath: https://github.com/stefankoegl/python-json-patch , https://github.com/h2non/jsonpath-ng -um exemplo simples: {"patch": [{"op": "Adicionar", "path": "metadata.name", "value": "testar"}, {"op": "Adicionar", "path": "metadata.array", "value": [1, 2, 3]}]} Por favor, incluir a chave de "patch" e que o valor seja uma matriz de patches que você pretende fazer.  Ele será executado como tal. A more complex example: {"patch": [{"op": "replace", "path": "$.spec.pools[?(@.spec.type == 'Master')]..endpoints","value": {"name": "New Endpoint"}}]}
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