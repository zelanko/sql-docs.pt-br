---
title: "Protegendo a replica&#231;&#227;o na Internet | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "segurança [replicação do SQL Server], Internet"
  - "Internet [replicação do SQL Server], segurança"
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Protegendo a replica&#231;&#227;o na Internet
  A replicação na Internet pode fornecer flexibilidade, principalmente para Assinantes móveis, mas você deve configurar a replicação na Internet de maneira adequada para garantir proteção adequada. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda usar uma de duas técnicas para compartilhar informações com segurança na Internet:  
  
-   Rede virtual privada (VPN)  
  
-   Opção de sincronização da Web para replicação de mesclagem  
  
## Rede Virtual Privada  
 As redes virtuais privadas fornecem uma abordagem sobreposta simples e segura para replicar dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na Internet. A conexão VPN pela Internet opera logicamente como um link WAN (Rede de Longa Distância) entre os sites.  
  
 Isso é obtido, permitindo que o usuário faça o encapsulamento pela Internet ou outra rede pública usando um protocolo como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Point Tunneling Protocol (PPTP) disponível com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT versão 4.0 ou [!INCLUDE[msCoName](../../../includes/msconame-md.md)] sistema operacional Windows 2000 ou o Layer Two Tunneling Protocol (L2TP) disponíveis com o sistema operacional Windows 2000. Esse processo fornece segurança e recursos semelhantes para aqueles disponíveis em uma rede privada.  
  
 Para obter mais informações sobre a configuração de uma VPN, consulte a documentação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows.  
  
## Sincronização da Web por IIS  
 A opção de sincronização da web para replicação de mesclagem fornece a capacidade de replicar dados usando o protocolo HTTPS, que pode ser uma abordagem conveniente para replicar dados através de um firewall. Para obter mais informações, consulte [Configurar sincronização da Web](../../../relational-databases/replication/configure-web-synchronization.md) e [arquitetura de segurança para sincronização da Web](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## Consulte também  
 [Práticas recomendadas em relação à segurança de replicação](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Segurança e proteção e 40; Replicação e 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  