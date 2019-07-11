---
title: referência de seção de configuração de bdc mssqlctl
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de seção de configuração mssqlctl bdc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3ca96ddbbf64b04e8ccd8854a8338fe6e118debb
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728699"
---
# <a name="mssqlctl-bdc-config-section"></a>seção de configuração do bdc mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para o **seção de configuração do bdc** comandos na **mssqlctl** ferramenta. Para obter mais informações sobre outros **mssqlctl** comandos, consulte [mssqlctl referência](reference-mssqlctl.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[Mostrar de seção de configuração de bdc mssqlctl](#mssqlctl-bdc-config-section-show) | Obtém uma seção de um perfil de configuração.
[conjunto de seção de configuração de bdc mssqlctl](#mssqlctl-bdc-config-section-set) | Define uma seção para um perfil de configuração.
## <a name="mssqlctl-bdc-config-section-show"></a>Mostrar de seção de configuração de bdc mssqlctl
Obtém a seção especificada do perfil config selecionado de acordo com o caminho json especificado.
```bash
mssqlctl bdc config section show --json-path -j 
                                 --config-profile -c  
                                 [--target -t]  
                                 [--force -f]
```
### <a name="examples"></a>Exemplos
Obtém um valor no final de um caminho de chave json simples.
```bash
mssqlctl bdc config section show --config-profile custom-config --json-path 'metadata.name' --target section.json
```
Obtém um valor no final de um caminho de chave json com uma condicional
```bash
mssqlctl bdc config section show --config-profile custom-config  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--json-path -j`
O caminho da chave json que leva para o valor desejado ou a seção do arquivo de JSON do perfil de configuração, ou seja, key1.key2.key3. Usa a linguagem de consulta jsonpath, https://github.com/h2non/jsonpath-ng, por exemplo: -j ' $. spec.pools [? ( @.spec.type = = "Mestre")]... pontos de extremidade
#### `--config-profile -c`
Caminho de perfil de configuração do BDC.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Caminho do arquivo de onde você deseja que o arquivo de seção colocado. Padrão: direcionado para stdout.
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
## <a name="mssqlctl-bdc-config-section-set"></a>conjunto de seção de configuração de bdc mssqlctl
Define a seção especificada no perfil de configuração selecionado acordo com o caminho json especificado.  Todos os examplesbelow são fornecidos no Bash.  Se usar outra linha de comando, esteja ciente de que você talvez precise escapequotations adequadamente.  Como alternativa, você pode usar a funcionalidade do arquivo de patch.
```bash
mssqlctl bdc config section set --config-profile -c 
                                [--json-values -j]  
                                [--patch-file -p]
```
### <a name="examples"></a>Exemplos
Ex. 1 (embutido) - defina a porta de um único ponto de extremidade (ponto de extremidade de controlador).
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values '$.spec.controlPlane.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ex. 1 (patch) - defina a porta de um único ponto de extremidade (ponto de extremidade de controlador) com o arquivo de patch.
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Por exemplo, 2 (embutido) - armazenamento de plano de controle de conjunto.
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values 'spec.controlPlane.spec.storage=spec.controlPlane.spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Por exemplo, 2 (patch) - armazenamento de plano de controle de conjunto com o arquivo de patch.
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"spec.controlPlane.spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3(inline) - defina armazenamento de pool, incluindo réplicas (Pool de armazenamento).
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
Por exemplo, 3 (patch) - defina pools de armazenamento, incluindo réplicas (Pool de armazenamento) com o arquivo de patch.
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-profile -c`
Caminho de perfil de configuração do BDC da configuração que você deseja definir para
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--json-values -j`
Uma lista de pares de valor de chave de caminhos de json para valores: key1.subkey1=value1,key2.subkey2=value2. Você pode fornecer embutido valores json, como: key ='{"tipo": "cluster", "name": "test-cluster"}' ou forneça um caminho de arquivo, como key=./values.json. Se você quiser definir um valor que requer uma condicional, use a notação de jsonpath por a partir de seu caminho com um $. Isso permitirá que você faça uma condicional, como -j $. key1.key2 [? ( @.key3= = 'Algumvalor'] .key4 = valor. Você pode ver exemplos abaixo. Para obter ajuda adicional, consulte: https://jsonpath.com/
#### `--patch-file -p`
Caminho para um arquivo json de patch que é baseado na biblioteca do jsonpatch: http://jsonpatch.com/. Você deve iniciar seu arquivo de patch json com uma chave chamada "patch", cujo valor é uma matriz de operações de patch que você pretende fazer. Para o caminho de uma operação de patch, você pode usar a notação de ponto, como key1.key2 para a maioria das operações. Se você gostaria de fazer uma operação de substituição, e você estiver substituindo um valor em uma matriz que requer uma condicional, use a notação de jsonpath por a partir de seu caminho com um $. Isso permitirá que você faça uma condicional, como $. key1.key2 [? ( @.key3= = 'Algumvalor'] .key4. Consulte os exemplos a seguir. Para obter ajuda adicional, consulte: https://jsonpath.com/.
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