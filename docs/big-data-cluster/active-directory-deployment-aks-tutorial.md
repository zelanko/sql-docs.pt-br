---
title: Implantação no Active Directory no AKS (Serviço de Kubernetes do Azure) – tutorial
titleSuffix: SQL Server Big Data Cluster
description: Saiba como implantar Clusters de Big Data do SQL Server no modo AD no AKS (Serviço de Kubernetes do Azure).
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b24a83e1647b0e32aff3ce19ad69a0fdc9405b0e
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632925"
---
# <a name="tutorial-deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>Tutorial: Implantar Clusters de Big Data do SQL Server no modo AD no AKS (Serviço de Kubernetes do Azure)

Este artigo explica como implantar um BDC (cluster de Big Data) do SQL Server no modo de autenticação do Active Directory com uma arquitetura de referência. A arquitetura de referência estende o AD DS (Active Directory Domain Services) local para o Azure. Implante-a por meio do [Centro de Arquitetura do Azure](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain) com os [blocos de construção do Azure](https://github.com/mspnp/template-building-blocks/wiki/Install-Azure-Building-Blocks).

## <a name="prerequisites"></a>Pré-requisitos

Antes de implantar um cluster de Big Data do SQL Server, você precisará:

* Acessar uma VM do Azure para gerenciamento. Essa VM exige acesso à VNet (Rede Virtual) do Azure em que você implantará o BDC. Ela precisa residir na mesma VNet ou em uma [VNet emparelhada](/azure/virtual-network/virtual-network-manage-peering).
* [Instalar as ferramentas de Big Data](deploy-big-data-tools.md) na VM de gerenciamento.
* Preparar a implantação do cluster no [modo de autenticação do Active Directory](active-directory-prerequisites.md) no controlador do AD local.

## <a name="create-aks-subnet"></a>Criar a sub-rede do AKS

1. Definir variáveis de ambiente

   ```console
   export REGION_NAME=< your Azure Region >
   export RESOURCE_GROUP=<your resource group >
   export SUBNET_NAME=aks-subnet
   export VNet_NAME= adds-vnet
   export AKS_NAME= <your aks cluster name>
   ```

1. Criar a sub-rede do AKS

   ```console
   SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNet_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
   ```

A captura de tela a seguir mostra como planejamos as sub-redes que residem na VNet na arquitetura.

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="Cluster do AKS com o AD e o Cluster de Big Data do SQL Server":::

## <a name="create-an-aks-private-cluster"></a>Criar um cluster privado do AKS

Use o comando a seguir para implantar o cluster privado do AKS. Caso você não precise de um cluster privado, remova o parâmetro `--enable-private-cluster` do comando. Para obter informações sobre outros requisitos, confira [Como implantar um AKS (Cluster do Kubernetes do Azure)](/azure/aks/tutorial-kubernetes-deploy-cluster).

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.3.0.10 \
    --service-cidr 10.3.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

Depois de implantar um cluster do AKS, [conecte-se ao cluster do AKS](/azure/aks/tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl).

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>Verificar a entrada DNS inversa para o controlador de domínio

Antes de iniciar a implantação do BDC no modo AD no cluster do AKS, verifique se o próprio controlador de domínio tem o **registro A** e o **registro PTR** (entrada DNS inversa) registrados no servidor DNS.

Para verificar essa configuração, execute o comando `nslookup` ou [o script do PowerShell](troubleshoot-ad-reverse-lookup-zone.md) para confirmar se você tem a entrada DNS inversa (registro PTR) configurada.

## <a name="create-bdc-deployment-profile"></a>Criar um perfil de implantação do BDC

O seguinte comando cria um perfil de implantação:

```console
azdata bdc config init --source kubeadm-prod  --target bdc-ad-aks
```

Os comandos a seguir são utilizados para definir parâmetros para um perfil de implantação.

### <a name="controljson"></a>control.json

```console
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.logs.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].dnsName=controller.contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].dnsName=proxys.contoso.com"

# security settings 
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"192.168.0.4\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"ad1.contoso.com\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainDnsName=contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
```

### <a name="bdcjson"></a>bdc.json

```console
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=master.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=mastersec.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=gateway.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=approxy.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="initiate-deployment"></a>Iniciar a implantação

O seguinte comando inicia uma implantação do BDC:

```console
azdata bdc create --config-profile bdc-ad-aks --accept-eula yes
```

## <a name="next-steps"></a>Próximas etapas

[Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md)

[Tutorial: Carregar dados de exemplo em um cluster de Big Data do SQL Server](tutorial-load-sample-data.md)