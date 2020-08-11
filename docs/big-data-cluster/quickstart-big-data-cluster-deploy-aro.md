---
title: Implantar no script de Python do Red Hat OpenShift no Azure
titleSuffix: SQL Server Big Data Clusters
description: Saiba como usar um script de implantação para implantar Clusters de Big Data do SQL Server no ARO (Red Hat OpenShift no Azure).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea5c622385b4350fb74362451eef3bb061d78fbc
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86160154"
---
# <a name="use-a-python-script-to-deploy-a-sql-server-big-data-cluster-on-azure-red-hat-openshift-aro"></a>Usar um script de Python para implantar um Cluster de Big Data do SQL Server no ARO (Red Hat OpenShift no Azure)

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Neste tutorial, você usa um exemplo de script de implantação de Python para implantar um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] no [ARO (Red Hat OpenShift no Azure)](/azure/virtual-machines/linux/openshift-get-started). Essa opção de implantação tem suporte começando no SQL Server 2019 CU5.

> [!TIP]
> O ARO é apenas uma opção para hospedar o Kubernetes para seu cluster de Big Data. Para saber mais sobre outras opções de implantação, bem como personalizar opções de implantação, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md).

A implantação padrão de cluster de Big Data usada aqui consiste em uma instância do SQL mestre, uma instância do pool de computação, duas instâncias do pool de dados e duas instâncias do pool de armazenamento. Os dados são persistidos usando volumes persistentes do Kubernetes que usam as classes de armazenamento padrão do ARO. A configuração padrão usada neste tutorial é adequada para ambientes de desenvolvimento/teste.

## <a name="prerequisites"></a>Pré-requisitos

- Uma assinatura do Azure.
- [oc](https://docs.openshift.com/container-platform/4.4/cli_reference/openshift_cli/getting-started-cli.html)
- [Versão mínima do Python 3.0](https://www.python.org/downloads)
- [`az` CLI](/cli/azure/install-azure-cli/)
- [`azdata` CLI](deploy-install-azdata.md)
- **Azure Data Studio**

## <a name="log-in-to-your-azure-account"></a>Faça logon na sua conta do Azure

O script usa a CLI do Azure para automatizar a criação de um cluster do ARO. Antes de executar o script, você deve fazer logon em sua conta do Azure com a CLI do Azure pelo menos uma vez. Execute o seguinte comando de um prompt de comando.

```terminal
az login
```

## <a name="instructions"></a>Instruções

1. Baixe o script de Python `deploy-sql-big-data-aro.py` e o arquivo YAML `bdc-scc.yaml`.

   >Esses arquivos estão localizados neste artigo em:
   - [`deploy-sql-big-data-aro.py`](#deploy-sql-big-data-aropy)
   - [`bdc-scc.yaml`](#bdc-sccyaml)

1. Execute o script usando:

```terminal
python deploy-sql-big-data-aro.py
```

Quando solicitado, forneça sua entrada para a ID da assinatura do Azure e o grupo de recursos do Azure no qual os recursos deverão ser criados. Opcionalmente, você também pode fornecer entradas para outras configurações ou usar os padrões fornecidos. Por exemplo:

- `azure_region`
- `vm_size` para nós de trabalho do OpenShift. Para ter a experiência ideal enquanto estiver validando cenários básicos, recomendamos pelo menos 8 vCPUs e 64 GB de memória em todos os nós de trabalho no cluster. O script usa `Standard_D8s_v3` e três 3 nós de trabalho como padrão. Uma configuração de tamanho padrão para Clusters de Big Data também usa cerca de 24 discos para declarações de volume persistentes em todos os componentes.
- Configuração de rede para implantação do cluster do OpenShift – confira o [artigo sobre a implantação do ARO](\azure\openshift\tutorial-create-cluster) para conhecer cada parâmetro com mais detalhes.
- `cluster_name` – esse valor é usado para o cluster do ARO e o Cluster de Big Data do SQL Server criado sobre o ARO. Observe que o nome do Cluster de Big Data do SQL será um namespace do Kubernetes.
- `username ` – esse é o nome de usuário para as contas provisionadas durante a implantação para a conta do administrador do controlador, a conta da instância mestra do SQL Server e o gateway. Observe que a conta do SQL Server `sa` é desabilitada automaticamente para você, como uma melhor prática.
- `password` – o mesmo valor será usado para todas as contas.

O Cluster de Big Data do SQL Server está implantado no ARO. Agora você pode usar Azure Data Studio para se conectar ao cluster. Para obter mais informações, confira [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md).

## <a name="clean-up"></a>Limpar

Se estiver testando o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Azure, exclua o cluster do ARO quando terminar para evitar encargos inesperados. Não remova o cluster se pretender continuar a usá-lo.

> [!WARNING]
> As etapas a seguir desmontam o cluster do ARO, o que também remove o cluster de Big Data do SQL Server. Se você tiver bancos de dados ou dados do HDFS que deseja manter, faça backup desses dados antes de excluir o cluster.

Execute o seguinte comando da CLI do Azure para remover o cluster de Big Data e o serviço do ARO no Azure (substitua `<resource group name>` pelo **grupo de recursos do Azure** especificado no script de implantação):

```terminal
az group delete -n <resource group name>
```

## `deploy-sql-big-data-aro.py` 

O script nesta seção implanta o Cluster de Big Data do SQL Server no Red Hat OpenShift no Azure. Copie o script para a estação de trabalho e salve-o como `deploy-sql-big-data-aro.py` antes de começar a implantação.

```python
#
# Prerequisites: 
# 
# Azure CLI (https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), azdata CLI (https://docs.microsoft.com/en-us/sql/big-data-cluster/deploy-install-azdata?view=sql-server-ver15), oc CLI (https://www.openshift.com/blog/installing-oc-tools-windows)
#
# Run `az login` at least once BEFORE running this script
#

from subprocess import check_output, CalledProcessError, STDOUT, Popen, PIPE, getoutput
from time import sleep
import os
import getpass
import json

def executeCmd (cmd):
    if os.name=="nt":
        process = Popen(cmd.split(),stdin=PIPE, shell=True)
    else:
        process = Popen(cmd.split(),stdin=PIPE)
    stdout, stderr = process.communicate()
    if (stderr is not None):
        raise Exception(stderr)

#
# MUST INPUT THESE VALUES!!!!!
#
SUBSCRIPTION_ID = input("Provide your Azure subscription ID:").strip()
GROUP_NAME = input("Provide Azure resource group name to be created:").strip()
#
# This password will be use for Controller user, Gateway user and SQL Server Master SA accounts
AZDATA_USERNAME=input("Provide username to be used for Controller, SQL Server and Gateway endpoints - Press ENTER for using  `admin`:").strip() or "admin"
AZDATA_PASSWORD = getpass.getpass("Provide password to be used for Controller user, Gateway user and SQL Server Master accounts:")
#
# Optionally change these configuration settings
#
AZURE_REGION=input("Provide Azure region - Press ENTER for using `westus2`:").strip() or "westus2"
# MASTER_VM_SIZE=input("Provide VM size for master nodes for the ARO cluster - Press ENTER for using  `Standard_D2s_v3`:").strip() or "Standard_D2s_v3"
WORKER_VM_SIZE=input("Provide VM size for the worker nodes for the ARO cluster - Press ENTER for using  `Standard_D8s_v3`:").strip() or "Standard_D8s_v3"
OC_NODE_COUNT=input("Provide number of worker nodes for ARO cluster - Press ENTER for using  `3`:").strip() or "3"
VNET_NAME=input("Provide name of Virtual Network for ARO cluster - Press ENTER for using  `aro-vnet`:").strip() or "aro-vnet"
VNET_ADDRESS_SPACE=input("Provide Virtual Network Address Space for ARO cluster - Press ENTER for using  `10.0.0.0/16`:").strip() or "10.0.0.0/16"
MASTER_SUBNET_NAME=input("Provide Master Subnet Name for ARO cluster - Press ENTER for using  `master-subnet`:").strip() or "master-subnet"
MASTER_SUBNET_IP_RANGE=input("Provide address range of Master Subnet for ARO cluster - Press ENTER for using  `10.0.0.0/23`:").strip() or "10.0.0.0/23"
WORKER_SUBNET_NAME=input("Provide Worker Subnet Name for ARO cluster - Press ENTER for using  `worker-subnet`:").strip() or "worker-subnet"
WORKER_SUBNET_IP_RANGE=input("Provide address range of Worker Subnet for ARO cluster - Press ENTER for using  `10.0.2.0/23`:").strip() or "10.0.2.0/23"
#
# This is both Kubernetes cluster name and SQL Big Data cluster name
CLUSTER_NAME=input("Provide name of OpenShift cluster and SQL big data cluster - Press ENTER for using  `sqlbigdata`:").strip() or "sqlbigdata"
#
# Deploy the ARO cluster
#  
print ("Set azure context to subscription: "+SUBSCRIPTION_ID)
command = "az account set -s "+ SUBSCRIPTION_ID
executeCmd (command)
print ("Creating azure resource group: "+GROUP_NAME)
command="az group create --name "+GROUP_NAME+" --location "+AZURE_REGION
executeCmd (command)
command = "az network vnet create --resource-group "+GROUP_NAME+" --name "+VNET_NAME+" --address-prefixes "+VNET_ADDRESS_SPACE
print("Creating Virtual Network: "+VNET_NAME)
executeCmd(command)
command = "az network vnet subnet create --resource-group "+GROUP_NAME+" --vnet-name "+VNET_NAME+" --name "+MASTER_SUBNET_NAME+" --address-prefixes "+MASTER_SUBNET_IP_RANGE+" --service-endpoints Microsoft.ContainerRegistry"
print("Creating Master Subnet: "+MASTER_SUBNET_NAME)
executeCmd(command)
command = "az network vnet subnet create --resource-group "+GROUP_NAME+" --vnet-name "+VNET_NAME+" --name "+WORKER_SUBNET_NAME+" --address-prefixes "+WORKER_SUBNET_IP_RANGE+" --service-endpoints Microsoft.ContainerRegistry"
print("Creating Worker Subnet: "+WORKER_SUBNET_NAME)
executeCmd(command)
command = "az network vnet subnet update --name "+MASTER_SUBNET_NAME+" --resource-group "+GROUP_NAME+" --vnet-name "+VNET_NAME+" --disable-private-link-service-network-policies true"
print("Updating Master Subnet by disabling Private Link Policies")
executeCmd(command)
command = "az aro create --resource-group "+GROUP_NAME+" --name "+CLUSTER_NAME+" --vnet "+VNET_NAME+" --master-subnet "+MASTER_SUBNET_NAME+" --worker-subnet "+WORKER_SUBNET_NAME+" --worker-count "+OC_NODE_COUNT+" --worker-vm-size "+WORKER_VM_SIZE +" --only-show-errors"
print("Creating OpenShift cluster: "+CLUSTER_NAME)
executeCmd (command)
#
# Login to oc console
#
command = "az aro list-credentials --name "+CLUSTER_NAME+" --resource-group "+GROUP_NAME +" --only-show-errors"
output=json.loads(getoutput(command))
OC_CLUSTER_USERNAME = str(output['kubeadminUsername'])
OC_CLUSTER_PASSWORD = str(output['kubeadminPassword'])
command = "az aro show --name "+CLUSTER_NAME+" --resource-group "+GROUP_NAME +" --only-show-errors"
output=json.loads(getoutput(command))
APISERVER = str(output['apiserverProfile']['url'])
command = "oc login "+ APISERVER+ " -u " + OC_CLUSTER_USERNAME + " -p "+ OC_CLUSTER_PASSWORD
executeCmd (command)
#
# Setup pre-requisites for deploying BDC on OpenShift
#
#
#Creating new project/namespace
command = "oc new-project "+ CLUSTER_NAME
executeCmd (command)
#
# create custom SCC for BDC
command = "oc apply -f bdc-scc.yaml"
executeCmd (command)
#
#Adding the custom scc to BDC namespace
command = "oc adm policy add-scc-to-group bdc-scc system:serviceaccounts:" + CLUSTER_NAME
executeCmd (command)
#
# Deploy big data cluster
#
print ('Set environment variables for credentials')
os.environ['AZDATA_PASSWORD'] = AZDATA_PASSWORD
os.environ['AZDATA_USERNAME'] = AZDATA_USERNAME
os.environ['ACCEPT_EULA']="Yes"
#
#Creating azdata configuration with aro-dev-test profile
command = "azdata bdc config init --source aro-dev-test --target custom --force"
executeCmd (command)
command="azdata bdc config replace -c custom/bdc.json -j ""metadata.name=" + CLUSTER_NAME + ""
executeCmd (command)
#
# Create BDC
command = "azdata bdc create --config-profile custom --accept-eula yes"
executeCmd(command)
#login into BDC cluster and list endpoints
command="azdata login -n " + CLUSTER_NAME
executeCmd (command)
print("")
print("SQL Server big data cluster endpoints: ")
command="azdata bdc endpoint list -o table"
executeCmd(command)
```

## `bdc-scc.yaml`

O manifesto .yaml a seguir define SCCs (restrições de contexto de segurança) personalizadas para a implantação do Cluster de Big Data. Copie-o para o mesmo diretório que `deploy-sql-big-data-aro.py`.

```yaml
allowHostDirVolumePlugin: false
allowHostIPC: false
allowHostNetwork: false
allowHostPID: false
allowHostPorts: false
allowPrivilegeEscalation: true
allowPrivilegedContainer: false
allowedCapabilities:
  - SETUID
  - SETGID
  - CHOWN
  - SYS_PTRACE
apiVersion: security.openshift.io/v1
defaultAddCapabilities: null
fsGroup:
  type: RunAsAny
kind: SecurityContextConstraints
metadata:
  annotations:
    kubernetes.io/description: SQL Server BDC custom scc is based on 'nonroot' scc plus additional capabilities required by BDC.
  generation: 2
  name: bdc-scc
readOnlyRootFilesystem: false
requiredDropCapabilities:
  - KILL
  - MKNOD
runAsUser:
  type: MustRunAsNonRoot
seLinuxContext:
  type: MustRunAs
supplementalGroups:
  type: RunAsAny
volumes:
  - configMap
  - downwardAPI
  - emptyDir
  - persistentVolumeClaim
  - projected
  - secret
```

## <a name="next-steps"></a>Próximas etapas

O script de implantação configurou o Serviço de Kubernetes do Azure e também implantou um cluster de Big Data do SQL Server 2019. Você também pode optar por personalizar implantações futuras por meio de instalações manuais. Para saber mais sobre como os clusters de Big Data são implantados e como personalizar implantações, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md).

Agora que o cluster de Big Data do SQL Server está implantado, você pode carregar dados de exemplo e explorar os tutoriais:

> [!div class="nextstepaction"]
> [Tutorial: Carregar dados de exemplo em um cluster de Big Data do SQL Server 2019](tutorial-load-sample-data.md)
