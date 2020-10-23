---
title: Referência do azdata arc postgres server config
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc postgres server config.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0c955a422d75e7f57fde2272675240e9b5337141
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358734"
---
# <a name="azdata-arc-postgres-server-config"></a>azdata arc postgres server config

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc postgres server config init](#azdata-arc-postgres-server-config-init) | Inicializa os o CRD e os arquivos de especificação de um grupo de servidores PostgreSQL.
[azdata arc postgres server config add](#azdata-arc-postgres-server-config-add) | Adicionar um valor para um caminho json em um arquivo de configuração.
[azdata arc postgres server config remove](#azdata-arc-postgres-server-config-remove) | Remover um valor para um caminho json em um arquivo de configuração.
[azdata arc postgres server config replace](#azdata-arc-postgres-server-config-replace) | Substituir um valor para um caminho json em um arquivo de configuração.
[azdata arc postgres server config patch](#azdata-arc-postgres-server-config-patch) | Corrigir um arquivo de configuração baseado em um arquivo de patch json.
## <a name="azdata-arc-postgres-server-config-init"></a>azdata arc postgres server config init
Inicializa os o CRD e os arquivos de especificação de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server config init --path -p 
                                       [--engine-version -ev]
```
### <a name="examples"></a>Exemplos
Inicializa os o CRD e os arquivos de especificação de um grupo de servidores PostgreSQL.
```bash
azdata arc postgres server config init --path ./template
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
Um caminho em que o CRD e a especificação do grupo de servidores PostgreSQL devem ser gravados.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--engine-version -ev`
Precisa ser 11 ou 12. O valor padrão é 12.
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
## <a name="azdata-arc-postgres-server-config-add"></a>azdata arc postgres server config add
Adiciona o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata arc postgres server config add --path -p 
                                      --json-values -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Adicionar armazenamento.
```bash
azdata arc postgres server config add --path custom/spec.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
Caminho para a especificação de recurso personalizado, ou seja, custom/spec.json
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
## <a name="azdata-arc-postgres-server-config-remove"></a>azdata arc postgres server config remove
Remove o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata arc postgres server config remove --path -p 
                                         --json-path -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Remover armazenamento.
```bash
azdata arc postgres server config remove --path custom/spec.json --json-path ".spec.storage"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
Caminho para a especificação de recurso personalizado, ou seja, custom/spec.json
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
## <a name="azdata-arc-postgres-server-config-replace"></a>azdata arc postgres server config replace
Substitui o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata arc postgres server config replace --path -p 
                                          --json-values -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Substituir a porta de um único ponto de extremidade.
```bash
azdata arc postgres server config replace --path custom/spec.json --json-values "$.spec.endpoints[?(@.name=="Controller")].port=30080"
```
Exemplo 2 – Substituir armazenamento.
```bash
azdata arc postgres server config replace --path custom/spec.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
Caminho para a especificação de recurso personalizado, ou seja, custom/spec.json
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
## <a name="azdata-arc-postgres-server-config-patch"></a>azdata arc postgres server config patch
Corrige o arquivo de configuração de acordo com o arquivo de patch fornecido. Confira http://jsonpatch.com/ para ter uma melhor compreensão de como os caminhos devem ser compostos. A operação de substituição pode usar condicionais em seu caminho devido à biblioteca de jsonpath https://jsonpath.com/. Todos os arquivos json de patch devem começar com uma chave de "patch" que tem uma matriz de patches com suas operações (adicionar, substituir, remover), caminho e valor correspondentes. A operação "remove" não requer um valor, apenas um caminho. Veja os exemplos abaixo.
```bash
azdata arc postgres server config patch --path -p 
                                        --patch-file
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Substituir a porta de um ponto de extremidade por um arquivo de patch.
```bash
azdata arc postgres server config patch --path custom/spec.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=="Controller")].port","value":30080}]}
```
Exemplo 2 – Substituir o armazenamento por um arquivo de patch.
```bash
azdata arc postgres server config patch --path custom/spec.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
Caminho para a especificação de recurso personalizado, ou seja, custom/spec.json
#### `--patch-file`
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

