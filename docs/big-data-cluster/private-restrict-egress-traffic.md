---
title: Restringir o tráfego de saída de clusters BDC (Clusters de Big Data) no cluster privado do AKS (Serviço de Kubernetes do Azure)
titleSuffix: SQL Server Big Data Clusters
description: Saiba como restringir o tráfego de saída de clusters BDC (Clusters de Big Data) no cluster privado do AKS (Serviço de Kubernetes do Azure).
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 962e155b3b0b5906d36fa4d884be2af353cb25a9
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076603"
---
# <a name="restrict-egress-traffic-of-big-data-clusters-bdc-clusters-in-azure-kubernetes-service-aks-private-cluster"></a>Restringir o tráfego de saída de clusters BDC (Clusters de Big Data) no cluster privado do AKS (Serviço de Kubernetes do Azure)

O AKS provisiona um SKU do Load Balancer padrão a ser configurada e usada para saída por padrão. No entanto, a configuração padrão poderá não cumprir os requisitos de todos os cenários se IPs públicos não forem permitidos ou saltos adicionais forem necessários para saída. Defina uma tabela de rotas definida pelo usuário se o cluster não permitir IPs públicos e ficar atrás de uma NVA (solução de virtualização de rede).

Por padrão, os clusters do AKS têm acesso irrestrito à Internet (saída) para fins de gerenciamento e operacionais. Os nós de trabalho em um cluster do AKS precisam acessar determinadas portas e FQDNs (nomes de domínio totalmente qualificados) para a instância:

* Atualizações de segurança do sistema operacional do nó de trabalho, o cluster precisa extrair imagens de contêiner do sistema base do MCR (Registro de Contêiner da Microsoft)
* Os nós de trabalho do AKS habilitados para GPU precisam acessar alguns pontos de extremidade do NVIDIA para instalar o driver
* No cenário em que os clientes usam o trabalho do AKS em conjunto com os serviços do Azure, como a política do Azure para conformidade de nível corporativo, Monitoramento do Azure (com insights de contêiner) 
* Espaço de Desenvolvimento habilitado e mais cenários de natureza semelhante

> [!NOTE]
> No momento, quando você implanta o BDC no cluster privado do AKS (Serviço de Kubernetes do Azure), não há dependência de entrada no cenário além das mencionadas neste artigo. Você pode encontrar todas as dependências de saída em [Controlar o tráfego de saída para nós do cluster no AKS (Serviço de Kubernetes do Azure)](/azure/aks/limit-egress-traffic).

Este artigo aborda como implantar o BDC no cluster privado do AKS com rede avançada e UDR (rota definida pelo usuário), bem como sua integração adicional ao ambiente de rede de nível corporativo.

## <a name="use-azure-firewall-to-restrict-egress-traffic"></a>Usar o firewall do Azure para restringir o tráfego de saída

O Firewall do Azure fornece uma marca FQDN `(AzureKubernetesService)` do Serviço de Kubernetes do Azure para simplificar essa configuração.

Confira [Restringir o tráfego de saída usando o Firewall do Azure](/azure/aks/limit-egress-traffic#restrict-egress-traffic-using-azure-firewall) para obter informações completas sobre essa marca.

A imagem a seguir mostra como o tráfego é restrito em um cluster privado do AKS. 

:::image type="content" source="media/private-cluster-restrict-egress-traffic/aks-azure-firewall-egress.png" alt-text="Tráfego de saída do firewall do cluster privado do AKS":::

Para configurar uma arquitetura básica com o Firewall do Azure:

1. Criar o grupo de recursos e a VNet
2. Criar e configurar o Firewall do Azure
3. Criar a tabela de rotas definidas pelo usuário
4. Configurar regras de firewall
5. Criar uma SP (entidade de serviço)
6. Criar um cluster privado do AKS
7. Criar um perfil de implantação do BDC
8. Implantar o BDC

As etapas a seguir fornecem detalhes.

## <a name="create-the-resource-group-and-vnet"></a>Crie o grupo de recursos e a VNet

1. Defina um conjunto de variáveis de ambiente para criar recursos.

   ```console
   export REGION_NAME=<region>
   export RESOURCE_GROUP=private-bdc-aksudr-rg
   export SUBNET_NAME=aks-subnet
   export VNET_NAME=bdc-vnet
   export AKS_NAME=bdcaksprivatecluster
   ```

1. Criar o grupo de recursos

   ```azurecli
   az group create -n $RESOURCE_GROUP -l $REGION_NAME
   ```

1. Criar a VNet

   ```azurecli
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
   ```

## <a name="create-and-set-up-azure-firewall"></a>Criar e configurar o Firewall do Azure

1. Defina um conjunto de variáveis de ambiente para criar recursos.

   ```console
   export FWNAME=bdcaksazfw
   export FWPUBIP=$FWNAME-ip
   export FWIPCONFIG_NAME=$FWNAME-config

   az extension add --name azure-firewall
   ```

1. Criar uma sub-rede dedicada para o firewall

   > [!NOTE]
   > Não é possível alterar o nome do firewall após a criação

   ```azurecli
   az network vnet subnet create \
     --resource-group $RESOURCE_GROUP \
     --vnet-name $VNET_NAME \
     --name AzureFirewallSubnet \
     --address-prefix 10.3.0.0/24

    az network firewall create -g $RESOURCE_GROUP -n $FWNAME -l $REGION_NAME --enable-dns-proxy true

    az network public-ip create -g $RESOURCE_GROUP -n $FWPUBIP -l $REGION_NAME --sku "Standard"

    az network firewall ip-config create -g $RESOURCE_GROUP -f $FWNAME -n $FWIPCONFIG_NAME --public-ip-address $FWPUBIP --vnet-name $VNET_NAME
   ```

Por padrão, o Azure roteia o tráfego automaticamente entre redes virtuais, redes locais e sub-redes do Azure. 

## <a name="create-user-defined-route-table"></a>Criar a tabela de rotas definidas pelo usuário

Crie uma tabela de UDR (rota definida pelo usuário) com um salto para o Firewall do Azure.

```azurecli

export SUBID= <your Azure subscription ID>
export FWROUTE_TABLE_NAME=bdcaks-rt
export FWROUTE_NAME=bdcaksroute
export FWROUTE_NAME_INTERNET=bdcaksrouteinet

export FWPUBLIC_IP=$(az network public-ip show -g $RESOURCE_GROUP -n $FWPUBIP --query "ipAddress" -o tsv)
export FWPRIVATE_IP=$(az network firewall show -g $RESOURCE_GROUP -n $FWNAME --query "ipConfigurations[0].privateIpAddress" -o tsv)

# Create UDR and add a route for Azure Firewall

az network route-table create -g $RESOURCE_GROUP --name $FWROUTE_TABLE_NAME

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME --route-table-name $FWROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FWPRIVATE_IP --subscription $SUBID

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME_INTERNET --route-table-name $FWROUTE_TABLE_NAME --address-prefix $FWPUBLIC_IP/32 --next-hop-type Internet
```

## <a name="set-up-firewall-rules"></a>Configurar regras de firewall 

```azurecli
# Add FW Network Rules

az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 1194 --action allow --priority 100
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 9000
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123

# Add FW Application Rules

az network firewall application-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwar' -n 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100
```

Você pode associar a tabela de UDR (rotas definidas pelo usuário) ao cluster do AKS em que o BDC implantado anteriormente usando o seguinte comando:

```azurecli
az network vnet subnet update -g $RESOURCE_GROUP --vnet-name $VNET_NAME --name $SUBNET_NAME --route-table $FWROUTE_TABLE_NAME
```

## <a name="create--configure-service-principal-sp"></a>Criar e configurar a SP (entidade de serviço)

Nesta etapa, você precisa criar a entidade de serviço e atribuir permissão à rede virtual.

Consulte o seguinte exemplo: 

```azurecli
# Create SP and Assign Permission to Virtual Network

az ad sp create-for-rbac -n "bdcaks-sp" --skip-assignment

APPID=<your service principal ID >
PASSWORD=< your service principal password >
VNETID=$(az network vnet show -g $RESOURCE_GROUP --name $VNET_NAME --query id -o tsv)

# Assign SP Permission to VNET

az role assignment create --assignee $APPID --scope $VNETID --role "Network Contributor"


RTID=$(az network route-table show -g $RESOURCE_GROUP -n $FWROUTE_TABLE_NAME --query id -o tsv)
az role assignment create --assignee $APPID --scope $RTID --role "Network Contributor"
```

## <a name="create-aks-cluster"></a>Criar cluster AKS

Em seguida, crie o cluster do AKS com `userDefinedRouting` como o tipo de saída.

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --outbound-type userDefinedRouting \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --service-principal $APPID \
    --client-secret $PASSWORD \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>Compilar perfil de implantação de BDC (Cluster de Big Data)

Você pode criar clusters BDC com o perfil personalizado: 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

## <a name="generate-and-config-bdc-custom-deployment-profile"></a>Gerar e configurar o perfil de implantação personalizada do BDC: 
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

## <a name="deploy-bdc-in-aks-private-cluster"></a>Implantar o BDC no cluster privado do AKS

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="use-third-party-firewall-instead-of-azure-firewall"></a>Usar o firewall de terceiros, em vez do Firewall do Azure

Use um firewall de terceiros para restringir o tráfego de saída quando o BDC é implantado com o cluster privado do AKS. Por exemplo, confira [Firewalls do Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps?search=firewall&page=1). Firewalls de terceiros podem ser usados em soluções de implantação privada com configurações mais em conformidade. O firewall deve fornecer as seguintes regras de rede:

* Todas as [regras de rede de saída necessárias e FQDNs para clusters do AKS](/azure/aks/limit-egress-traffic#required-outbound-network-rules-and-fqdns-for-aks-clusters) e todos os pontos de extremidade HTTP/HTTPS curingas e dependências que podem variar com o cluster AKS conforme vários qualificadores e seus requisitos reais.
* Regras de rede necessárias globais do Azure/FQDN/regras de aplicativo mencionadas [aqui](/azure/aks/limit-egress-traffic#azure-global-required-network-rules).
* FQDN recomendado opcional/regras de aplicativo para clusters do AKS mencionados [aqui](/azure/aks/limit-egress-traffic#optional-recommended-fqdn--application-rules-for-aks-clusters). 

Verifique como [gerenciar o BDC no cluster privado do AKS](private-manage.md). Então, a próxima etapa é [conectar-se ao cluster do BDC](connect-to-big-data-cluster.md).

Confira os scripts de automação para este cenário no [repositório de exemplos do SQL Server no GitHub](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks).

## <a name="next-steps"></a>Próximas etapas

[Gerenciar cluster de Big Data no cluster privado do AKS](private-manage.md)

[Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md)
