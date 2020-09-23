---
title: 'Grupos de disponibilidade Always On: interoperabilidade'
description: Descreve os diferentes recursos que podem e não podem funcionar junto com um grupo de disponibilidade Always On.
ms.custom: seodec18
ms.date: 04/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: reference
helpviewer_keywords:
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], interoperability
ms.assetid: daf87f90-2623-42ca-912c-b8f07d210510
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f0038fb53bb0f50dfd11551bed9a7c17a41971a1
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115713"
---
# <a name="always-on-availability-groups-interoperability-sql-server"></a>Grupos de disponibilidade Always On: interoperabilidade (SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Este tópico documenta interoperabilidade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] com outros recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].

## <a name="features-that-interoperate-with-always-on-availability-groups"></a><a name="Interop"></a> Recursos que interoperam com grupos de disponibilidade Always On

A tabela a seguir lista os recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que interoperam com [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Um link na coluna **Mais Informações** indica que existem considerações de interoperabilidade para um determinado recurso.

|Recurso|Mais informações|
|:------|:---------------|
|captura de dados de alterações|[Replicação, controle de alterações, Change Data Capture e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|
|controle de alterações|[Replicação, controle de alterações, Change Data Capture e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)|
|Bancos de dados independentes|[Bancos de dados independentes com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/contained-databases-with-always-on-availability-groups-sql-server.md)|
|Criptografia de banco de dados|[Bancos de dados criptografados com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)|
|Instantâneos de banco de dados|[Instantâneos do banco de dados com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/database-snapshots-with-always-on-availability-groups-sql-server.md)|
|FILESTREAM e FileTable|[FILESTREAM e FileTable com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)|
|Pesquisa de texto completo|Observação: os índices de texto completo são sincronizados com bancos de dados secundários Always On.|
|Envio de logs|[Pré-requisitos para migrar de envio de logs para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)|
|RBS (Armazenamento de Blob Remoto)|[RBS &#40;Repositório de Blob Remoto&#41; e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)|
|Replicação|[Configurar a replicação para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)<br /><br /> [Mantendo um banco de dados de publicação AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)<br /><br /> [Replicação, controle de alterações, Change Data Capture e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replicate-track-change-data-capture-always-on-availability.md)<br /><br /> [Assinantes de replicação e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)|
|Serviços de análise|[Analysis Services com grupos de disponibilidade AlwaysOn](../../../database-engine/availability-groups/windows/analysis-services-with-always-on-availability-groups.md)|
|Reporting Services|Utilize réplicas secundárias somente leitura como uma fonte de dados de relatório e reduza a carga em sua réplica de leitura/gravação primária.<br /><br /> [Reporting Services com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md)|
|Agente de Serviço|[Service Broker com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md)|
|SQL Server Agent|&nbsp;|

## <a name="features-that-interoperate-with-always-on-availability-groups-with-restrictions"></a><a name="restrictions"></a> Recursos que interoperam com Grupos de Disponibilidade AlwaysOn com restrições

Os seguintes recursos interoperam com [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] com restrições específicas. Consulte os tópicos vinculados para obter detalhes.

- Transações distribuídas/transações entre bancos de dados ([!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] e Windows Server 2016). Para obter mais informações, consulte [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)
- [Coletor de dados do sistema de estatísticas de consulta](../../../relational-databases/data-collection/system-data-collection-set-reports.md#Query) não pode ser executado de forma confiável em um ambiente com secundários não legíveis. Para usar o coletor de dados do sistema de estatísticas de consulta, defina todas as réplicas do grupo de disponibilidade para permitir [acesso de leitura](configure-read-only-access-on-an-availability-replica-sql-server.md). 

## <a name="features-that-do-not-interoperate-with-always-on-availability-groups"></a><a name="NoInterop"></a> Recursos que não interoperam com grupos de disponibilidade AlwaysOn

[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não interopera com os seguintes recursos:

- Espelhamento de banco de dados. Para obter mais informações, consulte [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).

## <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado

- **Blogs:**

  [Guia de migração: Migrando para o clustering de failover do SQL Server 2012 e os grupos de disponibilidade de implantações de clustering e espelhamento anteriores](https://blogs.msdn.microsoft.com/sqlalwayson/2012/04/09/now-available-migration-guide-migrating-to-sql-server-2012-failover-clustering-and-availability-groups-from-prior-clustering-and-mirroring-deployments/)
  [Blogs da Equipe de Always On do SQL Server: o Blob da Equipe de Always On do SQL Server oficial](https://blogs.msdn.microsoft.com/sqlalwayson/)
  [Blogs de Engenheiros do CSS SQL Server](https://docs.microsoft.com/archive/blogs/psssql/)

- **Whitepapers:**

  [Guia de migração: Migrando para Grupos de Disponibilidade Always On de implantações anteriores que combinam espelhamento de banco de dados e envio de logs](https://msdn.microsoft.com/library/jj635217)
  [Guia de soluções Always On do Microsoft SQL Server para alta disponibilidade e recuperação de desastres](https://go.microsoft.com/fwlink/?LinkId=227600)
  [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)
  [White papers da equipe de consultoria de cliente do SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)

## <a name="see-also"></a>Consulte Também

[Visão geral dos grupos de disponibilidade Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
[Pré-requisitos, restrições e recomendações para grupos de disponibilidade Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)
