---
title: "Publicar dados pela Internet usando VPN | Microsoft Docs"
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
  - "VPNs [replicação do SQL Server]"
  - "publicação na Web [replicação do SQL Server], VPNs"
  - "Internet [replicação do SQL Server], VPNs"
ms.assetid: 9ffb6546-9973-4574-aaa0-8fe0017e3601
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Publicar dados pela Internet usando VPN
  A tecnologia VPN (rede virtual privada) permite que usuários que trabalham em casa, filiais, clientes remotos e outras empresas se conectem a uma rede corporativa pela Internet, mantendo comunicações seguras. Os usuários podem usar a Autenticação do Windows como se estivessem em uma LAN (rede local). Todos os tipos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] replicação pode replicar dados através de uma VPN, mas considere o uso de sincronização da Web se você estiver usando replicação de mesclagem, como a sincronização da Web elimina a necessidade de uma VPN. Para obter mais informações, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
 A VPN inclui um software cliente de modo que os computadores são conectados pela Internet (ou, em casos especiais, até mesmo por uma intranet) a um software em um computador ou um servidor dedicado. Opcionalmente, se utiliza criptografia nas duas extremidades, assim como métodos de autenticação de usuário. A conexão VPN pela Internet opera logicamente como um link WAN (Rede de Longa Distância) entre os sites.  
  
 Uma VPN conecta os componentes de uma rede usando outra rede. Para conectar, o usuário trafega pela Internet ou outra rede pública usando um protocolo como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] PPTP (protocolo de encapsulamento ponto a ponto) ou L2TP (protocolo de encapsulamento de camada 2). Este processo provê a mesma segurança e os recursos previamente apenas disponíveis em uma rede privada. O PPTP é disponível com o Microsoft Windows NT version 4.0 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] 2000 (e posteriores) sistemas operacionais Windows; L2TP está disponível com o Windows 2000 e posterior.  
  
 Para o usuário, a infraestrutura de roteamento intermediário da Internet não é visível e parece que os dados estão sendo enviados por um link privado dedicado. Para os usuários, a VPN é uma conexão ponto a ponto entre o computador do usuário e um servidor corporativo.  
  
 Depois de você ter configurado o seu cliente remoto para conectar usando uma VPN e o cliente tenha acesso à Internet e se registre à LAN corporativa, você pode configurar a replicação como se o cliente remoto estivesse conectado diretamente na LAN. Por motivos de segurança, é possível ter diferentes recursos de rede disponíveis aos usuários conectados pela VPN e àqueles conectados diretamente pela LAN.  
  
 Para obter mais informações sobre a configuração de uma VPN, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## Consulte também  
 [Replicação na Internet](../../relational-databases/replication/replication-over-the-internet.md)  
  
  