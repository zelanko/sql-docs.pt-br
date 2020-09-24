---
title: Referência do azdata arc dc
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata arc dc.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 79798b8818a028edbe372e2a8cb341c5296582ba
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942242"
---
# <a name="azdata-arc-dc"></a>azdata arc dc

Aplica-se ao `azdata`

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata arc dc create](#azdata-arc-dc-create) | Criar um controlador de dados.
[azdata arc dc delete](#azdata-arc-dc-delete) | Excluir um controlador de dados.
[azdata arc dc endpoint](reference-azdata-arc-dc-endpoint.md) | Comandos de ponto de extremidade.
[azdata arc dc status](reference-azdata-arc-dc-status.md) | Comandos de status.
[azdata arc dc config](reference-azdata-arc-dc-config.md) | Comandos de configuração.
[azdata arc dc debug](reference-azdata-arc-dc-debug.md) | Comandos de depuração.
[azdata arc dc export](#azdata-arc-dc-export) | Exportar métricas, logs ou dados de uso.
[azdata arc dc upload](#azdata-arc-dc-upload) | Carregar arquivo de dados exportado.
## <a name="azdata-arc-dc-create"></a>azdata arc dc create
A configuração Criar um controlador de dados – configuração de kube é necessária em seu sistema, juntamente com as seguintes variáveis de ambiente ['AZDATA_USERNAME', 'AZDATA_PASSWORD'].
```bash
azdata arc dc create --namespace -ns 
                     --name -n  
                     
--connectivity-mode  
                     
--resource-group -g  
                     
--location -l  
                     
--subscription -s  
                     
[--profile-name]  
                     
[--path -p]  
                     
[--storage-class -sc]
```
### <a name="examples"></a>Exemplos
Implantação de controlador de dados.
```bash
azdata arc dc create
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--namespace -ns`
O namespace do Kubernetes no qual implantar o controlador de dados. Se um já existir, ele será usado. Se ele não existir, uma tentativa de criá-lo será feita primeiro.
#### `--name -n`
O nome do controlador de dados.
#### `--connectivity-mode`
A conectividade direta ou indireta com o Azure em que o controlador de dados deve operar.
#### `--resource-group -g`
O grupo de recursos do Azure no qual o recurso do controlador de dados deve ser adicionado.
#### `--location -l`
O local do Azure no qual os metadados do controlador de dados serão armazenados (por exemplo, eastus).
#### `--subscription -s`
A ID da assinatura do Azure na qual o recurso do controlador de dados deve ser adicionado.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--profile-name`
O nome de um perfil de configuração existente. Execute `azdata arc dc config list` para ver as opções disponíveis. Uma das seguintes: ['azure-arc-aks-premium-storage', 'azure-arc-ake', 'azure-arc-openshift', 'azure-arc-gke', 'azure-arc-aks-default-storage', 'azure-arc-kubeadm', 'azure-arc-eks', 'azure-arc-azure-openshift', 'azure-arc-aks-hci'].
#### `--path -p`
O caminho para um diretório que contém um perfil de configuração personalizado a ser usado. Execute `azdata arc dc config init` para criar um perfil de configuração personalizado.
#### `--storage-class -sc`
A classe de armazenamento a ser usada para todos os dados e volumes de logs persistentes para todos os pods do controlador de dados para os quais eles são necessários.
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
## <a name="azdata-arc-dc-delete"></a>azdata arc dc delete
Excluir o controlador de dados – a configuração de kube é necessária no seu sistema.
```bash
azdata arc dc delete --name -n 
                     --namespace -ns  
                     
[--force -f]
```
### <a name="examples"></a>Exemplos
Implantação de controlador de dados.
```bash
azdata arc dc delete
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--name -n`
Nome do controlador de dados.
#### `--namespace -ns`
O namespace do Kubernetes no qual o controlador de dados existe.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--force -f`
Forçar a exclusão do controlador de dados.
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
## <a name="azdata-arc-dc-export"></a>azdata arc dc export
Exportar métricas, logs ou uso para um arquivo.
```bash
azdata arc dc export --type -t 
                     --path -p  
                     
[--force -f]
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--type -t`
O tipo de dados a ser exportado. Opções: logs, métricas e uso.
#### `--path -p`
O caminho completo ou relativo, incluindo o nome do arquivo a ser exportado.
### <a name="optional-parameters"></a>Parâmetros Opcionais
#### `--force -f`
Forçar a criação do arquivo de saída. Substitui qualquer arquivo existente no mesmo caminho.
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
## <a name="azdata-arc-dc-upload"></a>azdata arc dc upload
Carregar arquivo de dados exportado de um controlador de dados para o Azure.
```bash
azdata arc dc upload --path -p 
                     
```
### <a name="required-parameters"></a>Parâmetros Exigidos
#### `--path -p`
O caminho completo ou relativo, incluindo o nome do arquivo a ser carregado.
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

