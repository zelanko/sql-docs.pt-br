---
title: Criar scripts de implantação para o Grupo de Disponibilidade Always On do SQL Server no Kubernetes
description: Este artigo explica como criar scripts de implantação para um Grupo de Disponibilidade Always On do SQL Server no Kubernetes
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 181773a19e87c34a1931cae05f5a329aedbc1239
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000136"
---
# <a name="create-deployment-script-for-sql-server-always-on-availability-group"></a>Criar script de implantação para o Grupo de Disponibilidade Always On do SQL Server

Este artigo descreve como implantar um grupo de disponibilidade em um cluster Kubernetes em um único comando com um script de implantação de exemplo. `deploy-ag.py` é um script Python que cria os arquivos `.yaml` para o cluster e pode aplicá-los a um cluster Kubernetes.

Baixe os arquivos em [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script).

## <a name="before-you-start"></a>Antes de iniciar

Instale as ferramentas a seguir em sua estação de trabalho.

* [Python](https://www.python.org/downloads/) (3.5 ou 3.6)
* [PyYAML](https://pyyaml.org/) – pacotes do Python
* [Cliente do Kubernetes](https://github.com/kubernetes-client/python) – pacote do Python

Adicione caminhos do Python às variáveis de ambiente (para o Windows).

### <a name="install-the-required-components"></a>Instalar os componentes necessários

O exemplo a seguir instala os pacotes do Cliente do Kubernetes e do PyYAML para o Python.

Depois de instalar o Python, baixe e extraia a pasta de exemplo. 

Para configurar os arquivos necessários, execute o comando a seguir. Substitua `<path>` pela localização dos arquivos de exemplo extraídos.

```cmd
pip install --user -r "C:\<path>\requirements.txt"
```

## <a name="create-cluster-and-download-config-file"></a>Criar um cluster e baixar o arquivo de configuração

O exemplo a seguir cria o cluster no AKS (Serviço de Kubernetes do Azure).

Antes de executar o script, atualize os valores entre colchetes angulares – `<>`.

```azcli
az aks create  --resource-group <GroupName> --name <ClusterName> --generate-ssh-keys --node-count 4 --kubernetes-version 1.11.1

az aks get-credentials --resource-group=<GroupName> --name=<ClusterName>
```

>[!NOTE]
>Os grupos de disponibilidade exigem o Kubernetes versão 1.11.0 ou superior. O exemplo especifica 1.11.1.

## <a name="run-the-deployment-script"></a>Executar o script de implantação

Os exemplos a seguir demonstram como executar `deploy-ag.py`.

### <a name="help"></a>Ajuda

```cmd
python ./deploy-ag.py --help
```

* **uso**: `deploy-ag.py [-h] {deploy | failover} ...`
* **argumentos opcionais**:
  * `-h, --help` mostrar esta mensagem de ajuda e sair
* **subcomandos**:
  * Ações no agente do k8s {implantar | fazer failover}

  `deploy`

   Implantar um conjunto de SQL Servers em um grupo de disponibilidade

  `failover`

   Fazer failover para uma réplica de destino.

### <a name="deploy-help"></a>Implantar a ajuda

```cmd
python ./deploy-ag.py deploy --help
```

* **uso**:

  ```
  python ./deploy-ag.py deploy [-h] [--verbose] [--ag AG] [-n NAMESPACE]
    [--dry-run] [-s SQL_SERVERS [SQL_SERVERS ...]]
    [-p SA_PASSWORD] [-e {ON_PREM,AKS}]
    [--skip-create-namespace]
  ```

  Implantar o SQL Server e agentes do k8s no namespace (nome do AG)

* **argumentos opcionais**:
  
  `-h, --help`
  
  mostrar esta mensagem de ajuda e sair
  
  `--verbose, -v`
  
  Detalhamento da saída
  
  `--ag AG`
  
  nome do grupo de disponibilidade. Default=ag1
  
  `-n NAMESPACE, --namespace NAMESPACE`
  
  nome do namespace do k8s. Usa como padrão o nome do AG se não é especificado.

  `--dry-run`
  
  Cria os manifestos, mas não os aplica.
  
  `-s SQL_SERVERS [SQL_SERVERS ...], --sql-servers SQL_SERVERS [SQL_SERVERS ...]`

  nomes de instâncias do SQL Server (até 5, separados por espaços) Padrão=['mssql1', 'mssql2', 'mssql3']
  
  `-p SA_PASSWORD, --sa-password SA_PASSWORD`
  
  Senha SA. Padrão='SAPassword2018'
  
  `-e {ON_PREM,AKS}, --env {ON_PREM,AKS}`
  
  `--skip-create-namespace`
  
  Ignora a criação do namespace.

### <a name="failover-help"></a>Ajuda de failover

```cmd
python ./deploy-ag.py failover --help
```
* **uso**: 

  ```cmd
  python deploy-ag.py failover [-h] [--verbose] [--ag AG]
    [--namespace NAMESPACE] [--dry-run]
    target_replica
  ```

  Failover manual

* **argumentos posicionais**: `target_replica`

  nome da réplica de destino do SQL Server para failover

* **argumentos opcionais**:

  `-h, --help`
  
  mostrar esta mensagem de ajuda e sair

  `--verbose, -v`
  
  Detalhamento da saída

  `--ag AG`
  
  nome do grupo de disponibilidade. Default=ag1

  `--namespace NAMESPACE`

  nome do namespace do k8s. Usa como padrão o nome do AG se não é especificado

  `--dry-run`
  
  Cria, mas não aplica os manifestos.

### <a name="create-the-manifests---dont-apply"></a>Criar os manifestos – não os aplicar

O script a seguir cria os arquivos de manifesto, mas não os aplica.

```cmd
python ./deploy-ag.py deploy --dry-run
```

O exemplo a seguir cria os manifestos para um grupo de disponibilidade no namespace `AG1` com três réplicas. Antes de executar o script, substitua `<MyC0m91exP@55w0r!>` por uma senha complexa.

```cmd
python ./deploy-ag.py deploy --ag ag1 --namespace AG1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --dry-run
```

O comando anterior gera o diretório de arquivos YAML de exemplo.

Nesse caso, a saída do comando mostra a localização na qual os arquivos de manifesto são criados.

![saída de script](./media/sql-server-linux-kubernetes-create-deployment/scriptbuild-out.png)
    
### <a name="create-the-manifests-and-apply"></a>Criar os manifestos e aplicá-los

O exemplo a seguir cria os manifestos para um grupo de disponibilidade no namespace `ag1` com três réplicas e aplica-os ao cluster Kubernetes. Em seguida, o cluster criará o grupo de disponibilidade. Antes de executar o script, substitua `<MyC0m91exP@55w0r!>` por uma senha complexa.

```
python ./deploy-ag.py deploy --ag ag1 --namespace ag1 --sa-password '<MyC0m91exP@55w0r!>' --env AKS --verbose
```

Após a conclusão do script, o operador do Kubernetes cria o armazenamento, as Instâncias do SQL Server e os serviços do balanceador de carga. Você pode monitorar a implantação com o [painel do Kubernetes](https://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Depois que o Kubernetes criar os contêineres do SQL Server:

1. [Conecte-se](sql-server-linux-kubernetes-connect.md) a uma instância do SQL Server no cluster.

1. Criar um banco de dados.

1. Faça um backup completo do banco de dados para iniciar a cadeia de logs.

1. Adicione um banco de dados ao grupo de disponibilidade.

O grupo de disponibilidade é criado com a propagação automática e, portanto, o SQL Server criará automaticamente os bancos de dados secundários nas réplicas apropriadas.

### <a name="manually-failover"></a>Failover manual

O exemplo a seguir faz failover da réplica primária.

```cmd
python ./deploy-ag.py failover --ag ag1 --namespace ag1 --verbose mssql1-0
```

## <a name="next-steps"></a>Próximas etapas

[Grupo de disponibilidade do SQL Server no cluster do Kubernetes](sql-server-ag-kubernetes.md)
