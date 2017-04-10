---
title: "Editores n&#227;o SQL Server | Microsoft Docs"
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
  - "replicação de banco de dados heterogênea, Publicadores não SQL Server"
  - "editores não SQL Server"
  - "fontes de dados heterogêneos, Publicadores não SQL Server"
  - "Publicadores [replicação do SQL Server], Oracle"
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Editores n&#227;o SQL Server
  Publicando dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fontes permite consolidar dados em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode se inscrever para instantâneo ou transacionais dados publicados a partir do banco de dados Oracle. Para obter mais informações sobre a publicação do Oracle, consulte [Visão geral da publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
 A replicação heterogênea para assinantes que não são do SQL Server foi preterida. A publicação Oracle foi preterida. Para mover dados, crie soluções usando a captura de dados de alterações e o [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Publicar de banco de dados não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é o ideal para os seguintes cenários:  
  
|Cenário|Descrição|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desenvolva com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver operando em dados replicados de banco de dados que não são do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Servidores de preparo de data warehouse|Manter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bancos de dados de preparo sincronizado com um não -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados.|  
|Migração para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Teste o seu aplicativo em tempo real com relação ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver reproduzindo as alterações do sistema de fonte. Alterne para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando estiver satisfeito com a migração.|  
  
## Consulte também  
 [Replicação de banco de dados heterogênea](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  