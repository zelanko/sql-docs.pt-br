---
title: Referência do azdata arc dc config
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc dc config.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 302235f43791f1be918f1e78114a40bcb23ea818
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942243"
---
# <a name="azdata-arc-dc-config"></a>azdata arc dc config

Aplica-se ao `azdata`

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc dc config init](#azdata-arc-dc-config-init) | Inicializa um perfil de configuração do controlador de dados que pode ser usado com control create.
[azdata arc dc config list](#azdata-arc-dc-config-list) | Lista opções de perfil de configuração disponíveis.
[azdata arc dc config add](#azdata-arc-dc-config-add) | Adicionar um valor para um caminho json em um arquivo de configuração.
[azdata arc dc config remove](#azdata-arc-dc-config-remove) | Remover um valor para um caminho json em um arquivo de configuração.
[azdata arc dc config replace](#azdata-arc-dc-config-replace) | Substituir um valor para um caminho json em um arquivo de configuração.
[azdata arc dc config patch](#azdata-arc-dc-config-patch) | Corrigir um arquivo de configuração baseado em um arquivo de patch json.
## <a name="azdata-arc-dc-config-init"></a>azdata arc dc config init
Inicializa um perfil de configuração de controlador de dados que pode ser usado com control create. A origem específica do perfil de configuração pode ser especificada nos argumentos.
```bash
azdata arc dc config init [--path -p] 
                          [--source -s]  
                          
[--force -f]
```
### <a name="examples"></a>Exemplos
Experiência de inicialização de configuração do controlador de dados orientada – você receberá prompts para obtenção dos valores necessários.
```bash
azdata arc dc config init
```
arc dc config init com argumentos, cria um perfil de configuração de aks-dev-test em ./custom.
```bash
azdata arc dc config init --source aks-dev-test --path custom
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--path -p`
Caminho do arquivo em que você deseja que o perfil de configuração seja colocado; o padrão é <cwd>/custom.
#### `--source -s`
Configurar origem do perfil: ['azure-arc-aks-premium-storage', 'azure-arc-ake', 'azure-arc-openshift', 'azure-arc-gke', 'azure-arc-aks-default-storage', 'azure-arc-aks-dev-test', 'azure-arc-kubeadm', 'azure-arc-kubeadm-dev-test', 'azure-arc-eks', 'azure-arc-azure-openshift', 'azure-arc-aks-hci']
#### `--force -f`
Forçar substituição do arquivo de destino.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-arc-dc-config-list"></a>azdata arc dc config list
Lista opções de perfil de configuração disponíveis para uso em `arc dc config init`
```bash
azdata arc dc config list [--config-profile -c] 
                          
```
### <a name="examples"></a>Exemplos
Mostra todos os nomes de perfis de configuração disponíveis.
```bash
azdata arc dc config list
```
Mostra o json de um perfil de configuração específico.
```bash
azdata arc dc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-profile -c`
Perfil de configuração padrão: ['azure-arc-aks-premium-storage', 'azure-arc-ake', 'azure-arc-openshift', 'azure-arc-gke', 'azure-arc-aks-default-storage', 'azure-arc-aks-dev-test', 'azure-arc-kubeadm', 'azure-arc-kubeadm-dev-test', 'azure-arc-eks', 'azure-arc-azure-openshift', 'azure-arc-aks-hci']
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-arc-dc-config-add"></a>azdata arc dc config add
Adiciona o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata arc dc config add --path -p 
                         --json-values -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Adicionar um armazenamento de controlador de dados.
```bash
azdata arc dc config add --path custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
O caminho do arquivo de configuração do controlador de dados da configuração que você gostaria de definir, ou seja, custom/control.json
#### `--json-values -j`
Uma lista de pares chave-valor de caminhos json para valores: key1.subkey1=value1,key2.subkey2=value2. Você pode fornecer valores json embutidos como: key='{"kind":"cluster","name":"test-cluster"}' ou fornecer um caminho de arquivo, como key=./values.json. Adicionar NÃO dá suporte a condicionais.  Se o valor embutido que você está fornecendo for um par chave-valor em si com "=" e ",", escape esses caracteres.  Por exemplo, key1="key2\=val2\,key3\=val3". Confira http://jsonpatch.com/ para obter exemplos de como deve ser a aparência de seu caminho.  Se quiser acessar uma matriz, você deverá fazer isso indicando o índice, como key.0=value
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-arc-dc-config-remove"></a>azdata arc dc config remove
Remove o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata arc dc config remove --path -p 
                            --json-path -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Remover um armazenamento do controlador de dados.
```bash
azdata arc dc config remove --path custom/control.json --json-path ".spec.storage"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
O caminho do arquivo de configuração do controlador de dados da configuração que você gostaria de definir, ou seja, custom/control.json
#### `--json-path -j`
Uma lista de caminhos json com base na biblioteca jsonpatch que indica os valores que você gostaria de remover, como: key1.subkey1,key2.subkey2. Remover NÃO dá suporte a condicionais. Confira http://jsonpatch.com/ para obter exemplos de como deve ser a aparência de seu caminho.  Se quiser acessar uma matriz, você deverá fazer isso indicando o índice, como key.0=value
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-arc-dc-config-replace"></a>azdata arc dc config replace
Substitui o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata arc dc config replace --path -p 
                             --json-values -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Substituir a porta de um único ponto de extremidade (ponto de extremidade do controlador de dados).
```bash
azdata arc dc config replace --path custom/control.json --json-values "$.spec.endpoints[?(@.name=="Controller")].port=30080"
```
Exemplo 2 – Substituir um armazenamento do controlador de dados.
```bash
azdata arc dc config replace --path custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
O caminho do arquivo de configuração do controlador de dados da configuração que você gostaria de definir, ou seja, custom/control.json
#### `--json-values -j`
Uma lista de pares chave-valor de caminhos json para valores: key1.subkey1=value1,key2.subkey2=value2. Você pode fornecer valores json embutidos como: key='{"kind":"cluster","name":"test-cluster"}' ou fornecer um caminho de arquivo, como key=./values.json. Substituir dá suporte a condicionais por meio da biblioteca jsonpath.  Para usar isso, inicie o caminho com um $. Isso permitirá que você faça uma condicional, como -j $.key1.key2[?(@.key3=="someValue"].key4=value. Se o valor embutido que você está fornecendo for um par chave-valor em si com "=" e ",", escape esses caracteres.  Por exemplo, key1="key2\=val2\,key3\=val3". Veja exemplos abaixo. Para obter ajuda adicional, confira: https://jsonpath.com/
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-arc-dc-config-patch"></a>azdata arc dc config patch
Corrige o arquivo de configuração de acordo com o arquivo de patch fornecido. Confira http://jsonpatch.com/ para ter uma melhor compreensão de como os caminhos devem ser compostos. A operação de substituição pode usar condicionais em seu caminho devido à biblioteca de jsonpath https://jsonpath.com/. Todos os arquivos json de patch devem começar com uma chave de "patch" que tem uma matriz de patches com suas operações (adicionar, substituir, remover), caminho e valor correspondentes. A operação "remove" não requer um valor, apenas um caminho. Veja os exemplos abaixo.
```bash
azdata arc dc config patch --path 
                           --patch-file -p
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Substituir a porta de um único ponto de extremidade (ponto de extremidade do controlador) com um arquivo de patch.
```bash
azdata arc dc config patch --path custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=="Controller")].port","value":30080}]}
```
Exemplo 2 – Substituir um armazenamento do controlador de dados com um arquivo de patch.
```bash
azdata arc dc config patch --path custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path`
O caminho do arquivo de configuração do controlador de dados da configuração que você gostaria de definir, ou seja, custom/control.json
#### `--patch-file -p`
Caminho para um arquivo json de patch que se baseia na biblioteca de jsonpatch: http://jsonpatch.com/. Você deve iniciar o arquivo json de patch com uma chave chamada "patch", cujo valor é uma matriz de operações de patch que você pretende fazer. Para o caminho de uma operação de patch, você pode usar a notação de ponto, como key1.key2, para a maioria das operações. Se você quiser fazer uma operação de substituição e estiver substituindo um valor em uma matriz que requer uma condicional, use a notação de jsonpath iniciando o caminho com um $. Isso permitirá que você faça uma condicional, como $.key1.key2[?(@.key3=="someValue"].key4. Veja os exemplos abaixo. Para obter ajuda adicional com os condicionais, confira https://jsonpath.com/.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).

