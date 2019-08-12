---
title: azdata bdc config reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1962fd25416ab3546c15f9b894375e0f3ed740c6
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894033"
---
# <a name="azdata-bdc-config"></a>azdata bdc config

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos **bdc config** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc config init](#azdata-bdc-config-init) | Inicializa um perfil de configuração do cluster de Big Data que pode ser usado com cluster create.
[azdata bdc config list](#azdata-bdc-config-list) | Lista opções de perfil de configuração disponíveis.
[azdata bdc config show](#azdata-bdc-config-show) | Mostra a configuração atual do BDC ou a configuração de um arquivo local que você especificar, ou seja, custom/cluster.json.
[azdata bdc config add](#azdata-bdc-config-add) | Adicionar um valor para um caminho json em um arquivo de configuração.
[azdata bdc config remove](#azdata-bdc-config-remove) | Remover um valor para um caminho json em um arquivo de configuração.
[azdata bdc config replace](#azdata-bdc-config-replace) | Substituir um valor para um caminho json em um arquivo de configuração.
[azdata bdc config patch](#azdata-bdc-config-patch) | Corrigir um arquivo de configuração baseado em um arquivo de patch json.
## <a name="azdata-bdc-config-init"></a>azdata bdc config init
Inicializa um perfil de configuração do cluster de Big Data que pode ser usado com cluster create. A origem específica do perfil de configuração pode ser especificada nos argumentos com três opções.
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Exemplos
Experiência de inicialização da configuração de BDC orientada – você receberá prompts para obter os valores necessários.
```bash
azdata bdc config init
```
Inicialização da configuração de BDC com argumentos, cria um perfil de configuração de aks-dev-test em./custom.
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Caminho do arquivo em que você deseja que o perfil de configuração seja colocado; o padrão é cwd com custom-config.json.
#### `--source -s`
Origem do perfil de configuração: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--force -f`
Forçar substituição do arquivo de destino.
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. 
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-config-list"></a>azdata bdc config list
Lista opções de perfil de configuração disponíveis para uso em `bdc config init`
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Exemplos
Mostra todos os nomes de perfis de configuração disponíveis.
```bash
azdata bdc config list
```
Mostra o json de um perfil de configuração específico.
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-profile -c`
Perfil de configuração padrão: ['aks-dev-test', 'kubeadm-dev-test', 'minikube-dev-test']
#### `--type -t`
O tipo de configuração que você gostaria de ver.
`cluster`
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. 
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-config-show"></a>azdata bdc config show
Mostra a configuração atual do BDC ou a configuração de um arquivo local que você especificar, ou seja, custom/cluster.json. O comando também poderá usar um caminho json se você quiser obter apenas uma seção.  Você também pode especificar um arquivo de destino para a saída.  Se um arquivo de destino não for especificado, ele será apenas uma saída para o terminal.
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       [--json-path -j]  
                       [--force -f]
```
### <a name="examples"></a>Exemplos
Mostrar a configuração do BDC no console
```bash
azdata bdc config show
```
Em um arquivo de configuração local, obtenha um valor no final de um caminho de chave json simples.
```bash
azdata bdc config show --config-file custom-config/cluster.json --json-path 'metadata.name' --target section.json
```
Em um arquivo de configuração local, obtém um valor no final de um caminho de chave json com uma condicional
```bash
azdata bdc config show --config-file custom-config/cluster.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-file -c`
Caminho do arquivo de configuração do cluster de Big Data se você não quiser a configuração do cluster ao qual está conectado, ou seja, custom/cluster.json
#### `--target -t`
Arquivo de saída no qual armazenar o resultado. Padrão: direcionado para stdout.
#### `--json-path -j`
O caminho de chave json que leva à seção ou ao valor desejado da configuração, ou seja, key1.key2.key3. Usa a linguagem de consulta jsonpath, https://jsonpath.com/, por exemplo: -j '$.spec.pools[?(@.spec.type == "Master")]..endpoints'
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-config-add"></a>azdata bdc config add
Adiciona o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Adicionar armazenamento de plano de controle.
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração do cluster de Big Data da configuração que você gostaria de definir, ou seja, custom/cluster.json
#### `--json-values -j`
Uma lista de pares chave-valor de caminhos json para valores: key1.subkey1=value1,key2.subkey2=value2. Você pode fornecer valores json embutidos como: key='{"kind":"cluster","name":"test-cluster"}' ou fornecer um caminho de arquivo, como key=./values.json. Adicionar NÃO dá suporte a condicionais.  Confira http://jsonpatch.com/ para obter exemplos de como deve ser a aparência de seu caminho.  Se quiser acessar uma matriz, você deverá fazer isso indicando o índice, como key.0=value
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-config-remove"></a>azdata bdc config remove
Remove o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Remover armazenamento de plano de controle.
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração do cluster de Big Data da configuração que você gostaria de definir, ou seja, custom/cluster.json
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
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-config-replace"></a>azdata bdc config replace
Substitui o valor no caminho json no arquivo de configuração.  Todos os exemplos abaixo são fornecidos em Bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário efetuar o escape das aspas.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Substituir a porta de um único ponto de extremidade (ponto de extremidade do controlador).
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Exemplo 2 – Substituir armazenamento de plano de controle.
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Exemplo 3 – Substituir o armazenamento do pool, incluindo réplicas (pool de armazenamento).
```bash
azdata bdc config replace --config-file custom/cluster.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração do cluster de Big Data da configuração que você gostaria de definir, ou seja, custom/cluster.json
#### `--json-values -j`
Uma lista de pares chave-valor de caminhos json para valores: key1.subkey1=value1,key2.subkey2=value2. Você pode fornecer valores json embutidos como: key='{"kind":"cluster","name":"test-cluster"}' ou fornecer um caminho de arquivo, como key=./values.json. Substituir dá suporte a condicionais por meio da biblioteca jsonpath.  Para usar isso, inicie o caminho com um $. Isso permitirá que você faça uma condicional, como -j $.key1.key2[?(@.key3=='someValue'].key4=value. Veja exemplos abaixo. Para obter ajuda adicional, confira: https://jsonpath.com/
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-bdc-config-patch"></a>azdata bdc config patch
Corrige o arquivo de configuração de acordo com o arquivo de patch fornecido. Confira http://jsonpatch.com/ para ter uma melhor compreensão de como os caminhos devem ser compostos. A operação de substituição pode usar condicionais em seu caminho devido à biblioteca de jsonpath https://jsonpath.com/. Todos os arquivos json de patch devem começar com uma chave de "patch" que tem uma matriz de patches com suas operações (adicionar, substituir, remover), caminho e valor correspondentes. A operação "remove" não requer um valor, apenas um caminho. Veja os exemplos abaixo.
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>Exemplos
Exemplo 1 – Substituir a porta de um único ponto de extremidade (ponto de extremidade do controlador) por um arquivo de patch.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Exemplo 2 – Substituir armazenamento de plano de controle por um arquivo de patch.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Exemplo 3 – Substituir o armazenamento do pool, incluindo réplicas (pool de armazenamento) por um arquivo de patch.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração do cluster de Big Data da configuração que você gostaria de definir, ou seja, custom/cluster.json
#### `--patch-file -p`
Caminho para um arquivo json de patch que se baseia na biblioteca de jsonpatch: http://jsonpatch.com/. Você deve iniciar o arquivo json de patch com uma chave chamada "patch", cujo valor é uma matriz de operações de patch que você pretende fazer. Para o caminho de uma operação de patch, você pode usar a notação de ponto, como key1.key2, para a maioria das operações. Se você quiser fazer uma operação de substituição e estiver substituindo um valor em uma matriz que requer uma condicional, use a notação de jsonpath iniciando o caminho com um $. Isso permitirá que você faça uma condicional, como $.key1.key2[?(@.key3=='someValue'].key4. Veja os exemplos abaixo. Para obter ajuda adicional com os condicionais, confira https://jsonpath.com/.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).