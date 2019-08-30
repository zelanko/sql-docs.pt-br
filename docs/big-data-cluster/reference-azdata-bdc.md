---
title: azdata bdc reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 408b3c2d55d5e2515a2df979cd54b380a0d54704
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155137"
---
# <a name="azdata-bdc"></a>bdc de azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

Este artigo é um artigo de referência para **azdata**. 

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | Criar cluster de Big Data.
[azdata bdc delete](#azdata-bdc-delete) | Excluir cluster de Big Data.
[azdata bdc config](reference-azdata-bdc-config.md) | Comandos de configuração.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | Comandos de ponto de extremidade.
[azdata bdc debug](reference-azdata-bdc-debug.md) | Comandos de depuração.
[azdata bdc status](reference-azdata-bdc-status.md) | Comandos de status do BDC.
[azdata bdc control](reference-azdata-bdc-control.md) | Comandos do serviço de controle.
[SQL BDC azdata](reference-azdata-bdc-sql.md) | Comandos do serviço SQL.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Comandos do serviço HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Comandos do serviço Spark.
[Gateway BDC do azdata](reference-azdata-bdc-gateway.md) | Comandos de serviço do gateway.
[aplicativo azdata BDC](reference-azdata-bdc-app.md) | Comandos do serviço de aplicativo.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | O módulo do HDFS fornece comandos para acessar um sistema de arquivos HDFS.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Os comandos do Spark permitem que o usuário interaja com o sistema Spark criando e gerenciando sessões, instruções e lotes.
## <a name="azdata-bdc-create"></a>azdata bdc create
Criar um SQL Server Cluster de Big data-a configuração kubernetes é necessária em seu sistema, juntamente com as seguintes variáveis de ambiente [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD '].
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>Exemplos
Experiência de implantação de BDC orientada – você receberá prompts para obter os valores necessários.
```bash
azdata bdc create
```
Implantação de BDC com argumentos.
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
Implantação de BDC com o nome especificado em vez do nome padrão no perfil.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```
Implantação de BDC com argumentos – nenhum prompt será fornecido, pois o sinalizador --Force será usado.
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do cluster de Big Data, usado para namespaces do Kubernetes.
#### `--config-profile -c`
Perfil de configuração de cluster de Big data, usado para implantar o cluster: [' AKs-dev-Test ', ' kubeadm-prod ', ' minikube-dev-Test ', ' kubeadm-dev-Test ']
#### `--accept-eula -a`
Você aceita os termos de licença? [sim/não]. Se não quiser usar esse argumento, você poderá definir a variável de ambiente ACCEPT_EULA como 'sim'. Os termos de licença desse produto podem ser exibidos em https://aka.ms/azdata-eula e https://go.microsoft.com/fwlink/?LinkId=2002534.
#### `--node-label -l`
Rótulo do nó de cluster de Big Data, usado para designar em quais nós implantar.
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
## <a name="azdata-bdc-delete"></a>azdata bdc delete
Exclua a configuração SQL Server Cluster de Big data-kubernetes é necessária no seu sistema.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Exemplos
Exclusão de BDC.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do cluster de Big Data, usado para namespaces de Kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--force -f`
Forçar exclusão do cluster de Big Data.
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
