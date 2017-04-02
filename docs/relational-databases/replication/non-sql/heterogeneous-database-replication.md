---
title: "Replica&#231;&#227;o de banco de dados heterog&#234;nea | Microsoft Docs"
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
  - "replicação de banco de dados heterogênea, sobre a replicação de banco de dados heterogênea"
  - "replicação [SQL Server], replicação de banco de dados heterogênea"
  - "replicação de banco de dados heterogênea"
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Replica&#231;&#227;o de banco de dados heterog&#234;nea
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte aos seguintes cenários heterogêneos para replicação transacional e de instantâneo:  
  
-   Publicando dados do Oracle no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Publicando dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para não assinantes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 A replicação heterogênea para assinantes que não são do SQL Server foi preterida. A publicação Oracle foi preterida. Para mover dados, crie soluções usando a captura de dados de alterações e o [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## Publicando dados do Oracle  
 Você pode usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para publicar dados do Oracle com grande parte dos mesmos recursos e a facilidade de uso do instantâneo do e das replicações transacionais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Publicando dados do Oracle é o ideal para os seguintes cenários:  
  
|Cenário|Descrição|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desenvolva com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver operando em dados replicados de banco de dados que não são do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Servidores de preparo de data warehouse|Manter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bancos de dados de preparo sincronizado com um não -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados.|  
|Migração para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Teste o seu aplicativo em tempo real com relação ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver reproduzindo as alterações do sistema de fonte. Alterne para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando estiver satisfeito com a migração.|  
  
 Para obter mais informações, consulte [Visão geral da publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## Publicando dados para assinantes não SQL Server  
 Os seguintes bancos de dados não [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com suporte como Assinantes para as publicações transacionais e instantâneos:  
  
-   Oracle para todas as plataformas que o Oracle oferece suporte.  
  
-   IBM DB2 para AS400, MVS, Unix, Linux e Windows.  
  
 Para obter mais informações, consulte [assinantes não-SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
  