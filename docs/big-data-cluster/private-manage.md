---
title: Gerenciar BDC (clusters de Big Data) no cluster privado do AKS (Serviço de Kubernetes do Azure)
titleSuffix: SQL Server Big Data Cluster
description: Saiba como gerenciar Clusters de Big Data do SQL Server no cluster privado do AKS (Serviço de Kubernetes do Azure).
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 442f5def7e1378b750460cfc6860e780b1dcfd80
ms.sourcegitcommit: fe5dedb2a43516450696b754e6fafac9f5fdf3cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89202190"
---
# <a name="manage-big-data-cluster-in-aks-private-cluster"></a>Gerenciar cluster de Big Data no cluster privado do AKS

Este artigo explica como gerenciar um cluster privado do AKS (Serviço de Kubernetes do Azure) com BDC (clusters de Big Data) do SQL Server implantados no Azure.

Conforme descrito em [Criar um cluster privado](/azure/aks/private-clusters/), o ponto de extremidade do servidor de API do cluster privado do AKS não tem nenhum endereço IP público. Para gerenciar o servidor de API, use uma VM que tenha acesso à VNet (rede virtual) do Azure do cluster AKS.

## <a name="azure-vm---same-vnet"></a>VM do Azure – mesma VNet

O método mais simples é implantar uma VM do Azure na mesma VNet que o cluster do AKS.

1. Implante uma VM do Azure na mesma VNET que o cluster do AKS. Às vezes, isso é chamado de *jumpbox*.
1. Conecte-se a essa VM e [Instale as ferramentas de Big Data do SQL Server 2019](deployment-guidance.md#install-sql-server-2019-big-data-tools).

Para fins de segurança, você pode usar os recursos do AKS para os intervalos de IP autorizados do servidor de API para limitar o acesso ao servidor de API (no Plano de Controle do AKS). O acesso limitado permite endereços IP específicos, como uma VM de jumpbox ou uma VM de gerenciamento, ou um intervalo de endereços IP para um grupo de desenvolvedores e o endereço IP público de front-end do firewall.

## <a name="other-options"></a>Outras opções

As alternativas ao uso de um jumpbox incluem:

* Usar uma VM em uma rede separada e configurar o [emparelhamento de rede virtual](/azure/virtual-network/virtual-network-peering-overview) para a VNet.

* Conexão do [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) ou [Gateway de VPN](/azure/vpn-gateway/vpn-gateway-about-vpngateways).

   [As opções para se conectar ao cluster privado](/azure/aks/private-clusters#options-for-connecting-to-the-private-cluster) discutem cada um dos métodos acima.

* Se o seu serviço for executado atrás de um [Azure Standard Load Balancer](/azure/aks/load-balancer-standard), ele poderá ser habilitado para [Link Privado do Azure](/azure/private-link/private-link-service-overview#limitations). Com o Link Privado do Azure, você pode habilitar o acesso privado de outras VNets do Azure.

* No cenário híbrido, você também pode configurar a conexão do [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) ou o [Gateway de VPN](/azure/vpn-gateway/vpn-gateway-about-vpngateways).

## <a name="next-steps"></a>Próximas etapas

[Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md)