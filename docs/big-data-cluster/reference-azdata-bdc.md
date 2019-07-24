---
title: referência do BDC do azdata
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos do BDC azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 488394cbf4b52a952ffc46ab2ec6c9a273466bd5
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426036"
---
# <a name="azdata-bdc"></a>BDC azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O artigo a seguir fornece referência para os comandos do **BDC** na ferramenta **azdata** . Para obter mais informações sobre outros comandos do **azdata** , consulte [referência do azdata](reference-azdata.md).

## <a name="commands"></a>Comandos

|     |     |
| --- | --- |
[criação de BDC do azdata](#azdata-bdc-create) | Criar cluster de Big Data.
[exclusão do BDC do azdata](#azdata-bdc-delete) | Exclua o cluster de Big Data.
[configuração do BDC do azdata](reference-azdata-bdc-config.md) | Comandos de configuração.
[ponto de extremidade do BDC azdata](reference-azdata-bdc-endpoint.md) | Comandos de ponto de extremidade.
[status do BDC azdata](reference-azdata-bdc-status.md) | Comandos de status.
[depuração do BDC azdata](reference-azdata-bdc-debug.md) | Comandos de depuração.
[controle BDC azdata](reference-azdata-bdc-control.md) | Comandos de controle.
[pool de BDC do azdata](reference-azdata-bdc-pool.md) | Comandos de pool.
[HDFS do BDC do azdata](reference-azdata-bdc-hdfs.md) | O módulo HDFS fornece comandos para acessar um sistema de arquivos HDFS.
[azdata BDC Spark](reference-azdata-bdc-spark.md) | Os comandos do Spark permitem que o usuário interaja com o sistema Spark criando e Gerenciando sessões, instruções e lotes.
## <a name="azdata-bdc-create"></a>criação de BDC do azdata
Criar um SQL Server Cluster de Big data – a configuração Kube é necessária em seu sistema, juntamente com as seguintes variáveis de ambiente [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD '].
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>Exemplos

Experiência de implantação do BDC orientada-você receberá prompts para obter os valores necessários.

```bash
azdata bdc create
```

Implantação do BDC com argumentos.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
Implantação do BDC com o nome especificado em vez do nome padrão no perfil.
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```

Implantação do BDC com argumentos-nenhum prompt será fornecido, pois o sinalizador--Force será usado.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```

### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do cluster de Big data, usado para namespaces kubernetes.
#### `--config-profile -c`
Perfil de configuração de cluster de Big data, usado para implantar o cluster: [' AKs-dev-Test ', ' kubeadm-dev-Test ', ' minikube-dev-Test ']
#### `--accept-eula -a`
Você aceita os termos de licença? [Sim/não]. Se você não quiser usar esse arg, poderá definir a variável de ambiente ACCEPT_EULA como ' Sim '. Os termos de licença deste produto podem ser exibidos em https://aka.ms/azdata-eula e https://go.microsoft.com/fwlink/?LinkId=2002534.
#### `--node-label -l`
Rótulo de nó de cluster de Big data, usado para designar em quais nós implantar.
#### `--force -f`
Forçar criação, o usuário não será solicitado a fornecer nenhum valor e todos os problemas serão impressos como parte do stderr.
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
## <a name="azdata-bdc-delete"></a>exclusão do BDC do azdata
Exclua a configuração SQL Server Cluster de Big data-Kube é necessária em seu sistema, juntamente com as seguintes variáveis de ambiente [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD '].
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>Exemplos
Exclusão do BDC em que o nome de usuário e a senha do controlador já estão definidos no ambiente do sistema.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>Parâmetros necessários
#### `--name -n`
Nome do cluster de Big data, usado para o namespace kubernetes.
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--force -f`
Forçar exclusão de Big Data cluster.
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
