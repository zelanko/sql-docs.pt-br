---
title: referência de controle azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos de controle azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2ce02ef0b212070b4a52944e055404137c78c98b
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304730"
---
# <a name="azdata-control"></a>controle azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[criação de controle azdata](#azdata-control-create) | Criar plano de controle.
[exclusão do controle azdata](#azdata-control-delete) | Excluir plano de controle.
## <a name="azdata-control-create"></a>criação de controle azdata
Criar plano de controle-a configuração Kube é necessária em seu sistema, juntamente com as seguintes variáveis de ambiente [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD '].
```bash
azdata control create [--name -n] 
                      [--config-profile -c]  
                      [--accept-eula -a]  
                      [--node-label -l]  
                      [--force -f]
```
### <a name="examples"></a>Exemplos
Implantação de controle.
```bash
azdata control create
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do plano de controle, usado para namespaces kubernetes.
#### `--config-profile -c`
Perfil de configuração de cluster, usado para implantar o cluster: [' AKs-dev-Test ', ' kubeadm-prod ', ' minikube-dev-Test ', ' kubeadm-dev-Test ']
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. 
#### `--node-label -l`
Rótulo do nó, usado para designar em quais nós implantar.
#### `--force -f`
Force a criação, não será solicitado que o usuário forneça nenhum valor e todos os problemas serão impressos como parte do stderr.
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
## <a name="azdata-control-delete"></a>exclusão do controle azdata
Excluir plano de controle-a configuração Kube é necessária no seu sistema.
```bash
azdata control delete --name -n 
                      [--force -f]
```
### <a name="examples"></a>Exemplos
Implantação de controle.
```bash
azdata control delete
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do plano de controle, usado para o namespace kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--force -f`
Forçar exclusão do plano de controle.
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

- Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

- Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
