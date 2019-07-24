---
title: referência de configuração do BDC azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos do BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed777391af3695da69e04c0e2693cff912c76771
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426286"
---
# <a name="azdata-bdc-config"></a>configuração do BDC do azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos de **configuração do BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[inicialização da configuração do BDC azdata](#azdata-bdc-config-init) | Inicializa um perfil de configuração de cluster de Big data que pode ser usado com o cluster Create.
[lista de configuração do BDC do azdata](#azdata-bdc-config-list) | Lista opções de perfil de configuração disponíveis.
[exibição da configuração do BDC do azdata](#azdata-bdc-config-show) | Mostra a configuração atual do BDC ou a configuração de um arquivo local que você especificar, ou seja, Custom/cluster. JSON.
[Adicionar azdata de configuração do BDC](#azdata-bdc-config-add) | Adicione um valor para um caminho JSON em um arquivo de configuração.
[remoção da configuração do BDC do azdata](#azdata-bdc-config-remove) | Remova um valor de um caminho JSON em um arquivo de configuração.
[substituição da configuração do BDC do azdata](#azdata-bdc-config-replace) | Substitua um valor para um caminho JSON em um arquivo de configuração.
[patch de configuração do BDC azdata](#azdata-bdc-config-patch) | Corrige um arquivo de configuração baseado em um arquivo de patch JSON.
## <a name="azdata-bdc-config-init"></a>inicialização da configuração do BDC azdata
Inicializa um perfil de configuração de cluster de Big data que pode ser usado com o cluster Create. A origem específica do perfil de configuração pode ser especificada nos argumentos de três opções.
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Exemplos
Experiência de inicialização de configuração do BDC guiada-você receberá prompts para obter os valores necessários.
```bash
azdata bdc config init
```
Config do BDC init com argumentos, cria um perfil de configuração de AKs-dev-Test em./Custom.
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--target -t`
Caminho do arquivo do qual você deseja que o perfil de configuração seja colocado, o padrão é CWD com Custom-config. JSON.
#### `--source -s`
Fonte do perfil de configuração: [' AKs-dev-Test ', ' kubeadm-dev-Test ', ' minikube-dev-Test ']
#### `--force -f`
Forçar substituição do arquivo de destino.
#### `--accept-eula -a`
Você aceita os termos de licença? [Sim/não]. Se você não quiser usar esse arg, poderá definir a variável de ambiente ACCEPT_EULA como ' Sim '. Os termos de licença deste produto podem ser exibidos em https://aka.ms/azdata-eula.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-config-list"></a>lista de configuração do BDC do azdata
Lista as opções de perfil de configuração disponíveis para uso no`bdc config init`
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>Exemplos
Mostra todos os nomes de perfil de configuração disponíveis.
```bash
azdata bdc config list
```
Mostra o JSON de um perfil de configuração específico.
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-profile -c`
Perfil de configuração padrão: [' AKs-dev-Test ', ' kubeadm-dev-Test ', ' minikube-dev-Test ']
#### `--type -t`
Qual tipo de configuração você gostaria de ver.
`cluster`
#### `--accept-eula -a`
Você aceita os termos de licença? [Sim/não]. Se você não quiser usar esse arg, poderá definir a variável de ambiente ACCEPT_EULA como ' Sim '. Os termos de licença deste produto podem ser exibidos em https://aka.ms/azdata-eula.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-config-show"></a>exibição da configuração do BDC do azdata
Mostra a configuração atual do BDC ou a configuração de um arquivo local que você especificar, ou seja, Custom/cluster. JSON. O comando também pode usar um caminho JSON se você quiser obter apenas uma seção.  Você também pode especificar um arquivo de destino para a saída.  Se um arquivo de destino não for especificado, ele será apenas uma saída para o terminal.
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
Em um arquivo de configuração local, obtenha um valor no final de um caminho de chave JSON simples.
```bash
azdata bdc config show --config-file custom-config/cluster.json --json-path 'metadata.name' --target section.json
```
Em um arquivo de configuração local, obtém um valor no final de um caminho de chave JSON com uma condicional
```bash
azdata bdc config show --config-file custom-config/cluster.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--config-file -c`
Caminho do arquivo de configuração de cluster de Big data se você não quiser a configuração do cluster no qual você está currentlylogged, ou seja, Custom/cluster. JSON
#### `--target -t`
Arquivo de saída no qual armazenar o resultado. Padrão: direcionado para stdout.
#### `--json-path -j`
O caminho de chave JSON que leva à seção ou ao valor desejado da configuração, ou seja, key1. Key2. key3. Usa a linguagem de consulta jsonpath https://jsonpath.com/ ,, por exemplo:-j ' $. spec. pools [? ( @.spec.type = = "Mestre")].. extremidade
#### `--force -f`
Forçar substituição do arquivo de destino.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-config-add"></a>Adicionar azdata de configuração do BDC
Adiciona o valor no caminho JSON no arquivo de configuração.  Todos os exemplos abaixo são fornecidos no bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário escapequotations adequadamente.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>Exemplos
Ex 1-adicionar armazenamento de plano de controle.
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração de cluster de Big data da configuração que você gostaria de definir, ou seja, Custom/cluster. JSON
#### `--json-values -j`
Uma lista de pares chave-valor de caminhos JSON para valores: key1. subkey1 = value1, Key2. subkey2 = value2. Você pode fornecer valores JSON embutidos como: Key = ' {"Kind": "cluster", "Name": "Test-cluster"} ' ou fornecer um caminho de arquivo, como key =./Values.JSON. Adicionar não oferece suporte a condicionais.  Consulte http://jsonpatch.com/ para obter exemplos de como deve ser a aparência de seu caminho.  Se você quiser acessar uma matriz, deverá fazer isso indicando o índice, como key. 0 = Value
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-config-remove"></a>remoção da configuração do BDC do azdata
Remove o valor no caminho JSON no arquivo de configuração.  Todos os exemplos abaixo são fornecidos no bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário escapequotations adequadamente.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>Exemplos
Ex 1-remover o armazenamento do plano de controle.
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração de cluster de Big data da configuração que você gostaria de definir, ou seja, Custom/cluster. JSON
#### `--json-path -j`
Uma lista de caminhos JSON com base na biblioteca jsonpatch que indica os valores que você gostaria de remover, como: key1. subkey1, Key2. subkey2. Remover não oferece suporte a condicionais. Consulte http://jsonpatch.com/ para obter exemplos de como deve ser a aparência de seu caminho.  Se você quiser acessar uma matriz, deverá fazer isso indicando o índice, como key. 0 = Value
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-config-replace"></a>substituição da configuração do BDC do azdata
Substitui o valor no caminho JSON no arquivo de configuração.  Todos os examplesbelow são fornecidos no bash.  Se estiver usando outra linha de comando, lembre-se de que talvez seja necessário escapequotations adequadamente.  Como alternativa, você pode usar a funcionalidade de arquivo de patch.
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>Exemplos
Por exemplo 1 – Substitua a porta de um único ponto de extremidade (ponto de extremidade do controlador).
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ex 2 – substituir o armazenamento do plano de controle.
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3-Substitua o armazenamento do pool, incluindo réplicas (pool de armazenamento).
```bash
azdata bdc config replace --config-file custom/cluster.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração de cluster de Big data da configuração que você gostaria de definir, ou seja, Custom/cluster. JSON
#### `--json-values -j`
Uma lista de pares chave-valor de caminhos JSON para valores: key1. subkey1 = value1, Key2. subkey2 = value2. Você pode fornecer valores JSON embutidos como: Key = ' {"Kind": "cluster", "Name": "Test-cluster"} ' ou fornecer um caminho de arquivo, como key =./Values.JSON. Replace dá suporte a condicionais por meio da biblioteca jsonpath.  Para usar isso, inicie o caminho com um $. Isso permitirá que você faça uma condicional, como-j $. key1. Key2 [? ( @.key3= = ' someValue ']. key4 = valor. Você pode ver exemplos abaixo. Para obter ajuda adicional, consulte: https://jsonpath.com/
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.
## <a name="azdata-bdc-config-patch"></a>patch de configuração do BDC azdata
Corrige o arquivo de configuração de acordo com o arquivo de patch fornecido. Consulte http://jsonpatch.com/ para obter uma melhor compreensão de como os caminhos devem ser compostos. A operação de substituição pode usar condicionais em seu caminho devido à biblioteca https://jsonpath.com/ jsonpath. Todos os arquivos JSON de patch devem começar com uma chave de "patch" que tem uma matriz de patches com seus op correspondentes (adicionar, substituir, remover), caminho e valor. O op "Remove" não requer um valor, apenas um caminho. Consulte os exemplos abaixo.
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>Exemplos
Ex. 1 – Substitua a porta de um único ponto de extremidade (ponto de extremidade do controlador) pelo arquivo de patch.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Ex 2 – Substitua o armazenamento do plano de controle pelo arquivo de patch.
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3-Substitua o armazenamento do pool, incluindo réplicas (pool de armazenamento) pelo arquivo de patch.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--config-file -c`
Caminho do arquivo de configuração de cluster de Big data da configuração que você gostaria de definir, ou seja, Custom/cluster. JSON
#### `--patch-file -p`
Caminho para um arquivo JSON de patch que se baseia na biblioteca jsonpatch: http://jsonpatch.com/. Você deve iniciar o arquivo JSON do patch com uma chave chamada "patch", cujo valor é uma matriz de operações de patch que você pretende fazer. Para o caminho de uma operação de patch, você pode usar a notação de ponto, como key1. Key2 para a maioria das operações. Se você quiser fazer uma operação de substituição e estiver substituindo um valor em uma matriz que requer uma condicional, use a notação jsonpath iniciando o caminho com um $. Isso permitirá que você faça uma condicional, como $. key1. Key2 [? ( @.key3= = ' someValue ']. key4. Consulte os exemplos abaixo. Para obter ajuda adicional com os condicionais, consulte https://jsonpath.com/:.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento de log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: JSON, jsonc, Table, TSV.  Padrão: JSON.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Consulte [http://jmespath.org/](http://jmespath.org/]) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento de log. Use--debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta **azdata** , consulte [instalar o azdata para gerenciar SQL Server 2019 Big data clusters](deploy-install-azdata.md).