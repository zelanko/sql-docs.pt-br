---
title: "Protegendo a replicação pela Internet | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d8ddd74c1e1e44c2b905a80b8e622d08a7758a5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="securing-replication-over-the-internet"></a>Protegendo a replicação na Internet
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A replicação na Internet pode fornecer flexibilidade, principalmente para Assinantes móveis, mas você deve configurar a replicação na Internet de maneira adequada para garantir proteção adequada. A[!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda usar uma de duas técnicas para compartilhar informações com segurança na Internet:  
  
-   Rede virtual privada (VPN)  
  
-   Opção de sincronização da Web para replicação de mesclagem  
  
## <a name="virtual-private-network"></a>Rede Virtual Privada  
 As redes virtuais privadas fornecem uma abordagem sobreposta simples e segura para replicar dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na Internet. A conexão VPN pela Internet opera logicamente como um link WAN (Rede de Longa Distância) entre os sites.  
  
 Isso é obtido permitindo que o usuário faça o encapsulamento pela Internet ou por meio de outra rede pública usando um protocolo como o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] PPTP (Point-to-Point Tunneling Protocol) disponível nos sistemas operacionais [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT versão 4.0 ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000 ou L2TP (Layer Two Tunneling Protocol) disponível no sistema operacional Windows 2000. Esse processo fornece segurança e recursos semelhantes para aqueles disponíveis em uma rede privada.  
  
 Para obter mais informações sobre a configuração de uma VPN, consulte a documentação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows.  
  
## <a name="web-synchronization-through-iis"></a>Sincronização da Web por IIS  
 A opção de sincronização da web para replicação de mesclagem fornece a capacidade de replicar dados usando o protocolo HTTPS, que pode ser uma abordagem conveniente para replicar dados através de um firewall. Para obter mais informações, consulte [Configurar sincronização da Web](../../../relational-databases/replication/configure-web-synchronization.md) e [Arquitetura de segurança para sincronização da Web](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## <a name="see-also"></a>Consulte também  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
