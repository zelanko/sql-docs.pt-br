---
title: 'Grupos de Disponibilidade AlwaysOn: interoperabilidade (SQL Server) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 55e19c050d0dd5d0a07c12f88076c423ade3281a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937197"
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Grupos de disponibilidade AlwaysOn: interoperabilidade (SQL Server)
  Este tópico documenta interoperabilidade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] com outros recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  

  
##  <a name="features-that-interoperate-with-alwayson-availability-groups"></a><a name="Interop"></a>Recursos que interoperam com o Grupos de Disponibilidade AlwaysOn  
 A tabela a seguir lista os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que interoperam com [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um link na coluna **Mais Informações** indica que existem considerações de interoperabilidade para um determinado recurso.  
  
|Recurso|Mais informações|  
|-------------|----------------------|  
|captura de dados de alterações|[Replicação, Controle de Alterações, captura de dados de alteração e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|Change tracking|[Replicação, Controle de Alterações, captura de dados de alteração e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)|  
|Bancos de dados independentes|[Bancos de dados independentes com grupos de disponibilidade AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)|  
|Criptografia de banco de dados|[Bancos de dados criptografados com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](encrypted-databases-with-always-on-availability-groups-sql-server.md)|  
|Instantâneos de banco de dados|[Instantâneos do banco de dados com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](database-snapshots-with-always-on-availability-groups-sql-server.md)|  
|FILESTREAM e FileTable|[FILESTREAM e Filetable com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|  
|Pesquisa de texto completo|Observação: os índices de texto completo são sincronizados com bancos de dados secundários AlwaysOn.|  
|Envio de logs|[Pré-requisitos para migrar do envio de logs para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|  
|RBS (Armazenamento de Blob Remoto)|[Remote BLOB Store &#40;RBS&#41; e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|  
|Replicação[Configurar replicação para grupos de disponibilidade AlwaysOn (SQL Server)](configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Mantendo um banco de dados de publicação AlwaysOn &#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [Replicação, Controle de Alterações, captura de dados de alteração e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [Assinantes de replicação e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)|  
|Analysis Services|[Analysis Services com grupos de disponibilidade AlwaysOn](analysis-services-with-always-on-availability-groups.md)|  
|Reporting Services|Utilize réplicas secundárias somente leitura como uma fonte de dados de relatório e reduza a carga em sua réplica de leitura/gravação primária.<br /><br /> [Reporting Services com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](reporting-services-with-always-on-availability-groups-sql-server.md)|  
|Agente de Serviço|[Service Broker com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](service-broker-with-always-on-availability-groups-sql-server.md)|  
|SQL Server Agent||  
  
##  <a name="features-that-do-not-interoperate-with-alwayson-availability-groups"></a><a name="NoInterop"></a>Recursos que não interoperam com Grupos de Disponibilidade AlwaysOn  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não interopera com os seguintes recursos:  
  
-   Transações envolvendo todos os bancos de dados/transações distribuídas  
  
     Para obter informações sobre por que não há suporte para essas transações, consulte [Transações envolvendo todos os bancos de dados sem suporte para espelhamento de banco de dados ou Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md).  
  
-   Espelhamento de banco de dados  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Guia de migração: Migrando para o clustering de failover do SQL Server 2012 e os grupos de disponibilidade de implantações de clustering e espelhamento anteriores](https://blogs.msdn.com/b/sqlalwayson/archive/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments.aspx)  
  
     [Blogs da equipe do SQL Server AlwaysOn: o blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Whitepapers:**  
  
     [Guia de migração: Migrando para grupos de disponibilidade AlwaysOn de implantações anteriores que combinam espelhamento de banco de dados e envio de logs](https://msdn.microsoft.com/library/jj635217)  
  
     [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
