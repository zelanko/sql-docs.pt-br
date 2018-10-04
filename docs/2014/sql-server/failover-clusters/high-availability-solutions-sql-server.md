---
title: Soluções de alta disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9b48d22e463b8596065c1df68d1affc0de5ef92a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091516"
---
# <a name="high-availability-solutions-sql-server"></a>Soluções de alta disponibilidade (SQL Server)
  Este tópico apresenta várias soluções de alta disponibilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que melhoram a disponibilidade de servidores ou bancos de dados. Uma solução de alta disponibilidade mascara os efeitos da falha de um hardware ou software e mantém a disponibilidade dos aplicativos, de modo a minimizar o tempo de inatividade percebido pelos usuários.  
  
> [!NOTE]  
>  Para obter informações sobre quais edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte a uma determinada solução de alta disponibilidade, consulte a seção “Alta disponibilidade (AlwaysOn)” de [Recursos compatíveis com as edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
(#RecommendedSolutions)  
  
##  <a name="TermsAndDefinitions"></a> Visão geral das soluções de alta disponibilidade do SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece várias opções para a criação de alta disponibilidade para um servidor ou banco de dados. As opções de alta disponibilidade incluem o seguinte:  
  
 Instâncias do cluster de failover do AlwaysOn  
 Como parte da oferta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn, as instâncias de cluster de failover do AlwaysOn aproveitam a funcionalidade WSFC (Windows Server Failover Clustering) para fornecer alta disponibilidade local por meio de redundância na instância de nível de servidor, uma FCI ( *instância de cluster de failover* ). Uma FCI é uma instância única do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é instalada em nós de WSFC (Windows Server Failover Clustering) e, possivelmente, em várias sub-redes. Na rede, uma FCI aparece ser uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sendo executada em um único computador, mas proporciona failover de um nó do WSFC para outro se o nó atual se tornar indisponível.  
  
 Para obter mais informações, consulte [ instâncias de Cluster de Failover do AlwaysOn (SQL Server)](windows/always-on-failover-cluster-instances-sql-server.md).  
  
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] é uma solução de alta disponibilidade no nível empresarial e recuperação de desastre introduzida no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para permitir que você maximize a disponibilidade para um ou mais bancos de dados de usuário. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] exige que as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] residam nos nós do WSFC (Clustering de Failover do Windows Server). Para obter mais informações, consulte [ grupos de disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).  
  
> [!NOTE]  
>  Uma FCI pode aproveitar os [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] para fornecer recuperação remota de desastres no nível do banco de dados. Para obter mais informações, consulte [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).  
  
 Espelhamento de banco de dados  
 > [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez dessa função, recomendamos usar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] .  
  
 O espelhamento de banco de dados é uma solução para aumentar a disponibilidade do banco de dados, dando suporte a failover quase instantâneo. O espelhamento de banco de dados pode ser usado para manter um único banco de dados de espera, ou *banco de dados espelho*, para um banco de dados de produção correspondente, que é referido como o *banco de dados principal*. Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Envio de logs  
 Como o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] e o espelhamento de banco de dados, o envio de logs opera no nível do banco de dados. Você pode usar o envio de logs para manter um ou mais bancos de dados de espera passiva (conhecidos como *bancos de dados secundários*) para um banco de dados de produção exclusivo, que é referenciado como o *banco de dados primário*. Para obter mais informações sobre o envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
##  <a name="RecommendedSolutions"></a> Soluções indicadas para usar o SQL Server para proteger dados  
 Nossa recomendação para fornecer proteção de dados para seu ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é a seguinte:  
  
-   Para proteção de dados por meio de uma solução de disco compartilhada de terceiros (uma rede SAN), nós recomendamos que você use as instâncias de cluster de failover AlwaysOn.  
  
-   Para obter proteção de dados por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recomendamos usar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
    > [!NOTE]  
    >  Se você estiver executando uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não dá suporte a [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], nós recomendaremos o envio de logs. Para obter informações sobre quais edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte ao [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], consulte a seção “Alta disponibilidade (AlwaysOn)” de [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte também  
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Espelhamento de banco de dados: interoperabilidade e coexistência &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)   
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2014](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
