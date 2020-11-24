---
title: Implantação no Active Directory no AKS (Serviço de Kubernetes do Azure)
titleSuffix: SQL Server Big Data Cluster
description: Explica conceitos e informações de planejamento sobre como implantar Clusters de Big Data do SQL Server no modo AD no AKS (Serviço de Kubernetes do Azure).
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3f6b3ce5f6a594e5be385ee1f7ea7d1c03c1f92a
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632929"
---
# <a name="deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>Implantar Clusters de Big Data do SQL Server no modo AD no AKS (Serviço de Kubernetes do Azure)

Os Clusters de Big Data do SQL Server dão suporte ao [modo de implantação AD (Active Directory)](deploy-active-directory.md) para o **IAM (Gerenciamento de Identidades e Acesso)** . O IAM para o **AKS (Serviço de Kubernetes do Azure)** foi um grande desafio, porque os protocolos padrão do setor, como o OAuth 2.0 e o OpenID Connect, que têm amplo suporte na plataforma de identidade da Microsoft não são compatíveis com o SQL Server.  

Este artigo explica como implantar um BDC (cluster de Big Data) no modo AD durante a implantação no [AKS (Serviço de Kubernetes do Azure)](/azure/aks/intro-kubernetes). 

## <a name="architecture-topologies"></a>Topologias de arquitetura

O **AD DS (Active Directory Domain Services)** é executado em uma VM (máquina virtual) do Azure [da mesma forma](/windows-server/identity/ad-ds/deploy/virtual-dc/adds-on-azure-vm) que é executado em muitas instâncias locais.  Depois de promover os novos controladores de domínio no Azure, defina os servidores DNS primários e secundários da rede virtual, rebaixe os servidores DNS locais que serão rebaixados para terciários ou inferiores. A autenticação do AD permite que clientes conectados ao domínio no [Linux se autentiquem no SQL Server](../linux/sql-server-linux-active-directory-auth-overview.md) usando as respectivas credenciais de domínio e o protocolo Kerberos.

Há algumas maneiras de implantar um BDC no modo AD no AKS.  Este artigo apresenta dois métodos, que são mais fáceis de serem implementados e integrados às arquiteturas de nível empresarial existentes:

* **Estender o seu domínio do Active Directory local para o Azure.** Esse método [permite que o seu ambiente do Active Directory](/azure/architecture/reference-architectures/identity/adds-extend-domain) forneça serviços de autenticação distribuídos usando o AD DS (Active Directory Domain Services) no Azure. Você replica o AD DS (Active Directory Domain Services) local para reduzir a latência causada pelo envio de solicitações de autenticação da nuvem novamente para o AD DS local. Um caso de uso típico dessa solução é quando seu aplicativo é hospedado parcialmente no local e parcialmente no Azure e suas solicitações de autenticação precisam ser enviadas bidirecionalmente.

   Veja como implantar essa solução passo a passo [nesta arquitetura de referência](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain).

* **Estenda a floresta de recursos do AD DS (Active Directory Domain Services) para o Azure.** Nessa arquitetura, você cria um domínio no Azure que é confiável para a floresta do AD local. Essa arquitetura mostra uma [relação de confiança unidirecional do domínio no Azure para a floresta local](/azure/architecture/reference-architectures/identity/adds-forest).

   A confiança permite que os usuários locais acessem recursos no domínio no Azure. Veja como implantar essa solução passo a passo [nesta arquitetura de referência](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-forest).

As arquiteturas de referência descritas acima permitem que você crie uma zona de destino, que tem todos os recursos a serem implantados do zero ou qualquer outra solução alternativa baseada na arquitetura existente. Além dessas arquiteturas de referência, você deve implantar o BDC em um cluster do AKS em uma sub-rede separada que permaneça na VNet de destino ou em uma VNet emparelhada.

A seguinte imagem representa uma arquitetura típica:

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="Cluster do AKS com o AD e o Cluster de Big Data do SQL Server":::

## <a name="recommendations"></a>Recomendações

As recomendações a seguir se aplicam à maioria das implantações do BDC no modo AD no AKS. As opções disponíveis serão mencionadas em cada componente a fim de fornecer diretrizes para melhor integração à arquitetura de nível empresarial.

### <a name="networking-recommendations"></a>Recomendações de rede

Alguns componentes básicos podem ser usados para conectar seu ambiente local ao Azure:

* **Gateway de VPN do Azure**: Um gateway de VPN é um tipo específico de gateway de rede virtual usado para enviar o tráfego criptografado entre uma rede virtual do Azure e um local na Internet pública. Você usará o Gateway de Rede Virtual do Azure e o Gateway de Rede Virtual local. Para obter informações sobre como configurá-los, confira [O que é o Gateway de VPN](/azure/vpn-gateway/vpn-gateway-about-vpngateways).
* **Azure ExpressRoute**: As conexões do ExpressRoute não passam pela Internet pública e oferecem mais segurança, confiabilidade e velocidades maiores com latências menores do que conexões típicas na Internet. A escolha da sua opção de conectividade afetará a latência, o desempenho e o nível de SLA da sua solução, dependendo dos SKUs. Para obter informações específicas, confira [Sobre os gateways de rede virtual do ExpressRoute](/azure/expressroute/expressroute-about-virtual-network-gateways).

A maioria dos clientes usa um jumpbox ou o [Azure Bastion](/azure/bastion/bastion-overview) para acessar outra infraestrutura do Azure. Com o **Link Privado do Azure**, você pode acessar com segurança os serviços de PaaS do Azure, incluindo o AKS nesse cenário, bem como outros serviços hospedados do Azure em um ponto de extremidade privado na sua rede virtual. O tráfego entre a rede virtual e o serviço percorre a rede de backbone da Microsoft, eliminando a exposição à Internet pública. Você também pode criar seu serviço de link privado na rede virtual e fornecê-lo de maneira privada aos clientes.

### <a name="active-directory-and-azure-recommendation"></a>Active Directory e recomendação do Azure

O AD DS local armazena informações sobre as contas de usuário e permite que outros usuários autorizados na mesma rede acessem essas informações autenticando identidades associadas a usuários, computadores, aplicativos ou outros recursos que estão incluídos em um limite de segurança. Na maioria dos cenários híbridos, a autenticação do usuário é executada em um Gateway de VPN ou uma conexão do ExpressRoute para o ambiente do AD DS local.  

Para uma implantação do BDC no modo AD, a solução usada para [integrar o Active Directory local ao Azure](/azure/architecture/reference-architectures/identity/) precisa ter os seguintes pré-requisitos:

* Uma [conta do AD tem permissão específica](active-directory-prerequisites.md) para criar usuários, grupos e contas de computador na UO (unidade organizacional) fornecida no Active Directory local.
* Um servidor DNS para [resolver o DNS interno](active-directory-dns-reconciliation.md). Ele precisa conter cria **registros do tipo A (pesquisa direta)** e **PTR (pesquisa inversa)** no servidor DNS com nomes nesse domínio. Especifique as configurações do DNS de domínio no perfil de implantação do BDC.  

## <a name="next-steps"></a>Próximas etapas

[Tutorial: Implantar Clusters de Big Data do SQL Server no modo AD no AKS (Serviço de Kubernetes do Azure)](active-directory-deployment-aks-tutorial.md)
