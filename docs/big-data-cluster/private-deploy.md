---
title: Implantar o BDC no cluster privado do AKS (Serviço de Kubernetes do Azure)
titleSuffix: SQL Server Big Data Cluster
description: Saiba como implantar Clusters de Big Data do SQL Server com o cluster privado do AKS (Serviço Kubernetes do Azure) com a rede avançada (CNI).
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4a55d7f6c9c55891f8d1a7bf97d8834c9df4a796
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283115"
---
# <a name="deploy-bdc-in-azure-kubernetes-service-aks-private-cluster"></a>Implantar o BDC no cluster privado do AKS (Serviço de Kubernetes do Azure)

Este artigo explica como implantar Clusters de Big Data do SQL Server no cluster privado do AKS (Serviço de Kubernetes do Azure). Essa configuração dá suporte ao uso restrito de endereços IP públicos no ambiente de rede corporativo.

Uma implantação privada oferece os seguintes benefícios:

* Uso restrito de endereços IP públicos
* O tráfego de rede entre servidores de aplicativos e pools de nó de cluster permanece apenas na rede privada
* Configuração personalizada para tráfegos de saída obrigatórios para atender a requisitos específicos

Este artigo demonstra como usar um cluster privado do AKS para restringir o uso do endereço IP público enquanto as respectivas cadeias de caracteres de segurança são aplicadas.

## <a name="deploy-private-bdc-cluster-with-aks-private-cluster"></a>Implantar o cluster privado do BDC com o cluster privado do AKS

Para começar, crie um [cluster privado do AKS](/azure/aks/private-clusters) para garantir que o tráfego de rede entre o servidor de API e os pools de nós permaneça somente na rede privada. O plano de controle ou o servidor de API tem endereços IP internos em um cluster privado do AKS.

Esta seção mostra como implantar um cluster do BDC no cluster privado do AKS (Serviço de Kubernetes do Azure) com a rede avançada (CNI).

## <a name="create-a-private-aks-cluster-with-advanced-networking"></a>Criar um cluster privado do AKS com rede avançada

```console

export REGION_NAME=<your Azure region >
export RESOURCE_GROUP=< your resource group name >
export SUBNET_NAME=aks-subnet
export VNET_NAME=bdc-vnet
export AKS_NAME=< your aks private cluster name >
 
az group create -n $RESOURCE_GROUP -l $REGION_NAME
 
az network vnet create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $VNET_NAME \
    --address-prefixes 10.0.0.0/8 \
    --subnet-name $SUBNET_NAME \
    --subnet-prefix 10.1.0.0/16
 

SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNET_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
 
echo $SUBNET_ID
## will be displayed something similar as the following: 
/subscriptions/xxxx-xxxx-xxx-xxxx-xxxxxxxx/resourceGroups/your-bdc-rg/providers/Microsoft.Network/virtualNetworks/your-aks-vnet/subnets/your-aks-subnet
```

### <a name="create-aks-private-cluster-with-advanced-networking-cni"></a>Criar um cluster privado do AKS com rede avançada (CNI)

Para poder avançar para a etapa a seguir, você precisa provisionar um cluster do AKS com Standard Load Balancer com recurso de cluster privado habilitado. O comando se parecerá com o seguinte: 

```console
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

Após uma implantação bem-sucedida, você pode ir para o grupo de recursos `<MC_yourakscluster>` e verá que `kube-apiserver` é um ponto de extremidade privado. Por exemplo, observe a seção a seguir.

## <a name="connect-to-an-aks-cluster"></a>Conectar-se a um cluster do AKS

```console
az aks get-credentials -n $AKS_NAME -g $RESOURCE_GROUP
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>Compilar perfil de implantação de BDC (Cluster de Big Data)

Depois de se conectar a um cluster do AKS, você pode começar a implantar o BDC, preparar a variável de ambiente e iniciar uma implantação: 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

Gerar e configurar o perfil de implantação personalizada do BDC:

```console
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.docker.imageTag=2019-CU6-ubuntu-16.04"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.logs.className=default"

azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"

azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="deploy-private-sql-server-big-data-cluster-with-ha"></a>Implantar o cluster de Big Data do SQL Server privado com HA

Caso você esteja [implantando um SQL-BDC (Cluster de Big Data do SQL Server) com HA (alta disponibilidade)](deployment-high-availability.md), usará a opção de implantar o perfil de implantação `aks-dev-test-ha`. Após uma implantação bem-sucedida, você poderá usar o mesmo comando `kubectl get svc` e verá que um serviço `master-secondary-svc` adicional é criado. É necessário configurar `ServiceType` como `NodePort`. Outras etapas serão semelhantes às mencionadas na seção anterior.

O seguinte exemplo define `ServiceType` como `NodePort`:

```console
azdata bdc config replace -c private-bdc-aks /bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
```

## <a name="deploy-bdc-in-aks-private-cluster"></a>Implantar o BDC no cluster privado do AKS

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="check-deployment-status"></a>Verifique o status da implantação

A implantação levará alguns minutos e você poderá usar o seguinte comando para verificar o status da implantação: 

```console
kubectl get pods -n mssql-cluster -w
```

## <a name="check-the-service-status"></a>Verificar o status do serviço

Use o comando a seguir para verificar os serviços. Verifique se todos estão íntegros sem IPs externos:

```console
kubectl get services -n mssql-cluster
```

Confira como [gerenciar o BDC no cluster privado do AKS](private-manage.md). Então, a próxima etapa é [conectar-se ao cluster do BDC](connect-to-big-data-cluster.md).

Confira os scripts de automação para este cenário no [repositório de exemplos do SQL Server no GitHub](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks).

## <a name="next-steps"></a>Próximas etapas

[Gerenciar um cluster privado](private-manage.md)

[Restringir o tráfego de saída do cluster privado do BDC](private-restrict-egress-traffic.md)

[Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md)
