---
title: "Solu&#231;&#245;es de alta disponibilidade (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "alta disponibilidade [SQL Server], soluções"
  - "Mecanismo de banco de dados [SQL Server], disponibilidade"
  - "disponibilidade do bancos de dados [SQL Server]"
  - "disponibilidade [SQL Server]"
  - "disponibilidade do servidor [SQL Server]"
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
caps.latest.revision: 84
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 84
---
# Solu&#231;&#245;es de alta disponibilidade (SQL Server)
  Este tópico apresenta várias soluções de alta disponibilidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que melhoram a disponibilidade de servidores ou bancos de dados. Uma solução de alta disponibilidade mascara os efeitos da falha de um hardware ou software e mantém a disponibilidade dos aplicativos, de modo a minimizar o tempo de inatividade percebido pelos usuários.    
    
   
>  **Observação:** Quer saber quais edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte a uma solução de alta disponibilidade específica? Confira a seção “Alta disponibilidade (AlwaysOn)” de [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).    
     
    
##  <a name="TermsAndDefinitions"></a> Visão geral das soluções de alta disponibilidade do SQL Server    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece várias opções para a criação de alta disponibilidade para um servidor ou banco de dados. As opções de alta disponibilidade incluem o seguinte:    
    
*  Instâncias do cluster de failover do AlwaysOn    
 Como parte da oferta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn, as Instâncias de Cluster de Failover do AlwaysOn aproveitam a funcionalidade WSFC (Windows Server Failover Clustering) para fornecer alta disponibilidade local por meio de redundância na instância de nível de servidor, uma FCI (*instância de cluster de failover*). Uma FCI é uma instância única do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é instalada em nós de WSFC (Windows Server Failover Clustering) e, possivelmente, em várias sub-redes. Na rede, uma FCI aparece ser uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sendo executada em um único computador, mas proporciona failover de um nó do WSFC para outro se o nó atual se tornar indisponível.    
    
 Para obter mais informações, consulte [Instâncias do cluster de failover do AlwaysOn &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).    
    
*  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] é uma solução de alta disponibilidade no nível empresarial e recuperação de desastre introduzida no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para permitir que você maximize a disponibilidade para um ou mais bancos de dados de usuário. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] exige que as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] residam nos nós do WSFC (Clustering de Failover do Windows Server). Para obter mais informações, confira [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).    
    
  
>  **Observação:** Uma FCI pode aproveitar os [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] para fornecer recuperação remota de desastres no nível do banco de dados. Para obter mais informações, veja [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).    
    
*  Espelhamento de banco de dados. **Observação:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez dessa função, recomendamos usar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].     
O espelhamento de banco de dados é uma solução para aumentar a disponibilidade do banco de dados, dando suporte a failover quase instantâneo. O espelhamento de banco de dados pode ser usado para manter um único banco de dados de espera, ou *banco de dados espelho*, para um banco de dados de produção correspondente, que é referido como o *banco de dados principal*. Para obter mais informações, consulte [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).    
    
*  Envio de logs    
 Como o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] e o espelhamento de banco de dados, o envio de logs opera no nível do banco de dados. Você pode usar o envio de logs para manter um ou mais bancos de dados de espera passiva (conhecidos como *bancos de dados secundários*) para um banco de dados de produção exclusivo, que é referenciado como o *banco de dados primário*. Para obter mais informações sobre o envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).    
    
##  <a name="RecommendedSolutions"></a> Soluções indicadas para usar o SQL Server para proteger dados    
 Nossa recomendação para fornecer proteção de dados para seu ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:    
    
-   Para obter proteção de dados por meio de uma solução de disco compartilhada de terceiros (uma rede SAN), recomendamos que você use as Instâncias de Cluster de Failover AlwaysOn.    
    
-   Para obter proteção de dados por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recomendamos usar [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].    
    
       >  É recomendável usar o envio de logs se você estiver executando uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não dá suporte a [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Para obter informações sobre quais edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte ao [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], confira a seção “Alta disponibilidade (AlwaysOn)” de [Recursos com suporte nas edições do SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).    
    
## Consulte também    
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)     
 [Espelhamento de banco de dados: interoperabilidade e coexistência &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)     
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)    
    
  