---
title: "Replicação de banco de dados heterogênea | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6eee43a7755f2e018a7ed4e9f822983b03b7181a
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="heterogeneous-database-replication"></a>replicação de banco de dados heterogênea
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte aos seguintes cenários heterogêneos para replicação transacional e de instantâneo:  
  
-   Publicando dados do Oracle no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Publicando dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para não assinantes do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 A replicação heterogênea para assinantes que não são do SQL Server foi preterida. A publicação Oracle foi preterida. Para mover dados, crie soluções usando a captura de dados de alterações e o [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>Publicando dados do Oracle  
 Você pode usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para publicar dados do Oracle com grande parte dos mesmos recursos e a facilidade de uso do instantâneo do e das replicações transacionais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Publicando dados do Oracle é o ideal para os seguintes cenários:  
  
|Cenário|Descrição|  
|--------------|-----------------|  
|Implantações de aplicativos do[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desenvolva com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver operando em dados replicados de banco de dados que não são do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Servidores de preparo de data warehouse|Mantenha os bancos de dados de preparo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizado com um banco de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migração para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Teste o seu aplicativo em tempo real com relação ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver reproduzindo as alterações do sistema de fonte. Alterne para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando estiver satisfeito com a migração.|  
  
 Para obter mais informações, consulte [Visão geral da publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>Publicando dados para assinantes não SQL Server  
 Os seguintes bancos de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com suporte como Assinantes para as publicações transacionais e instantâneos:  
  
-   Oracle para todas as plataformas que o Oracle oferece suporte.  
  
-   IBM DB2 para AS400, MVS, Unix, Linux e Windows.  
  
 Para obter mais informações, consulte [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
  
