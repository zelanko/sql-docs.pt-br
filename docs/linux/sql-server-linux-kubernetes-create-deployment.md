---
title: Criar scripts de implantação para o SQL Server sempre no grupo de disponibilidade no Kubernetes
description: Este artigo explica como criar scripts de implantação para um SQL Server sempre no grupo de disponibilidade no Kubernetes
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6541cae5271e35fd5ad0030ffc8625fc97a46149
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231139"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>Criar script de implantação para o SQL Server sempre no grupo de disponibilidade

Este artigo descreve como implantar um grupo de disponibilidade em um cluster Kubernetes em um único comando com um exemplo de script de implantação. `deploy-ag.py` é um script Python que cria o `.yaml` arquivos para o cluster e aplicá-las a um cluster Kubernetes.

Download de arquivos de arquivos do [exemplos do sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script).

## <a name="before-you-start"></a>Antes de iniciar

Instale as ferramentas a seguir em sua estação de trabalho.

* [Python](https://www.python.org/downloads/) (3.5 ou 3.6)
* [PyYAML](https://pyyaml.org/) -pacotes do Python
* [Cliente de Kubernetes](https://github.com/kubernetes-client/python) -pacote do Python

Adicione caminhos de python às variáveis de ambiente (para Windows).

### <a name="install-the-required-components"></a>Instalar os componentes necessários

O exemplo a seguir acima instala os pacotes de cliente de Kubernetes e PyYAML para Python.

Depois de instalar o Python, baixe e extraia a pasta de exemplo. 

Para configurar os arquivos necessários, execute o comando a seguir. Substitua `<path>` com o local dos arquivos de amostra extraída.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>Criar Cluster e baixe o arquivo de configuração

O exemplo a seguir cria o cluster no serviço de Kubernetes do Azure (AKS).

Antes de executar o script, atualize os valores entre colchetes angulares - `<>`.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>Grupos de disponibilidade requer Kubernetes versão 1.11.0 ou superior. O exemplo especifica 1.11.1.

## <a name="run-the-deployment-script"></a>Execute o script de implantação

Os exemplos a seguir demonstram como executar `deploy-ag.py`.

### <a name="help"></a>Help

```cmd
python ./deploy-ag.py --help
```

* **uso**: `deploy-ag.py [-h] {deploy | failover} ...`
* **argumentos opcionais**:
  * `-h, --help` Mostrar esta mensagem de Ajuda e sair
* **subcommands**:
  * Ações no agente k8s {implantar | failover}

  `deploy`

   Implantar um conjunto de servidores SQL em um grupo de disponibilidade

  `failover`

   Fazer failover para uma réplica de destino.

### <a name="deploy-help"></a>Implantar a Ajuda

```cmd
python ./deploy-ag.py deploy --help
```

* **usage**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  Implantar o SQL Server e os agentes de k8s namespace(AG name)

* **argumentos opcionais**:
  
  `-h, --help`
  
  Mostrar esta mensagem de Ajuda e sair
  
  `--verbose, -v`
  
  Detalhamento da saída
  
  `--ag AG`
  
  nome do grupo de disponibilidade. Default=ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  nome do namespace k8s. O padrão é nome do grupo de disponibilidade se não for especificado.

  `--dry-run`
  
  Criar os manifestos, mas não aplicá-las.
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  nomes de instâncias do SQL Server (até 5, separados por espaços), padrão = ['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  Senha de SA. Default='SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  Ignorar a criação do namespace.

### <a name="failover-help"></a>Ajuda de failover

```cmd
python ./deploy-ag.py failover --help
```
* **usage**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  Faça failover manualmente

* **argumentos posicionais**: `target_replica`

  nome da réplica do SQL Server de destino para failover

* **argumentos opcionais**:

  `-h, --help`
  
  Mostrar esta mensagem de Ajuda e sair

  `--verbose, -v`
  
  Detalhamento da saída

  `--ag AG`
  
  nome do grupo de disponibilidade. Default=ag1

  `--namespace NAMESPACE`

  nome do namespace k8s. O padrão é nome do grupo de disponibilidade se não especificado

  `--dry-run`
  
  Criar, mas não se aplicam os manifestos.

### <a name="create-the-manifests---dont-apply"></a>Criar os manifestos – não se aplicam

O script a seguir cria os arquivos de manifesto, mas não aplicá-las.

```cmd
python ./deploy-ag.py deploy --dry-run
```

O exemplo a seguir cria os manifestos para um grupo de disponibilidade em namespace `AG1` com três réplicas. Antes de executar o script, substitua `<MyC0m91exP@55w0r!>` com uma senha complexa.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

O comando anterior gera o diretório de arquivos de exemplo yaml.

Nesse caso, a saída do comando mostra onde os arquivos de manifesto são criados.

![Saída do script](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>Os manifestos de criar e aplicar

O exemplo a seguir cria os manifestos para um grupo de disponibilidade em namespace `ag1` com três réplicas e aplica-se ao cluster Kubernetes. O cluster, em seguida, criará o grupo de disponibilidade. Antes de executar o script, substitua `<MyC0m91exP@55w0r!>` com uma senha complexa.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

Depois que o script for concluído, o operador de Kubernetes cria o armazenamento, as instâncias do SQL Server, os serviços do balanceador de carga. Você pode monitorar a implantação com [painel do Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Depois que o Kubernetes cria os contêineres do SQL Server:

1. [Conectar-se](sql-server-linux-kubernetes-connect.md) para uma instância do SQL Server no cluster.

1. Criar um banco de dados.

1. Faça um backup completo do banco de dados para iniciar a cadeia de log.

1. Adicione o banco de dados para o grupo de disponibilidade.

O grupo de disponibilidade é criado com a propagação automática para que o SQL Server criará automaticamente os bancos de dados secundários nas réplicas apropriadas.

### <a name="manually-failover"></a>Faça failover manualmente

O exemplo a seguir faz failover da réplica primária.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>Próximas etapas

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
