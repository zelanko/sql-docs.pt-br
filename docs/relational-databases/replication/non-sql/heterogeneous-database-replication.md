---
description: replicação de banco de dados heterogênea
title: Replicação de banco de dados heterogênea | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d5ea494a48932fac171eb4d9e8bc3e032001e55b
ms.sourcegitcommit: 821e7039a342bf76306d66c61db247dc2caabc46
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "96999224"
---
# <a name="heterogeneous-database-replication"></a>replicação de banco de dados heterogênea  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte aos seguintes cenários heterogêneos para replicação transacional e de instantâneo:  
  
-   Publicando dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para não assinantes do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  

-   A publicação de dados para e do Oracle tem as seguintes restrições:  

  |Cenário|2016 ou anterior |2017 ou posterior |
  |-------|-------|--------|
  |Replicação do Oracle |Dá suporte apenas ao Oracle 10g ou anterior |Dá suporte apenas ao Oracle 10g ou anterior |
  |Replicação para o Oracle |Todas as versões anteriores ao Oracle 12c |Sem suporte |


 A replicação heterogênea para assinantes que não são do SQL Server foi preterida. A publicação Oracle foi preterida. Para mover dados, crie soluções usando a captura de dados de alterações e o [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>Publicando dados do Oracle  
 Você pode usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para publicar dados do Oracle com grande parte dos mesmos recursos e a facilidade de uso do instantâneo do e das replicações transacionais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Este recurso requer o Oracle versão 10G ou anterior. Publicando dados do Oracle é o ideal para os seguintes cenários:  
  
|Cenário|Descrição|  
|--------------|-----------------|  
|Implantações de aplicativos do[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desenvolva com o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver operando em dados replicados de banco de dados que não são do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Servidores de preparo de data warehouse|Mantenha os bancos de dados de preparo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizado com um banco de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migração para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Teste o seu aplicativo em tempo real com relação ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enquanto estiver reproduzindo as alterações do sistema de fonte. Alterne para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando estiver satisfeito com a migração.|  
  
 Para obter mais informações, consulte [Visão geral da publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>Publicando dados para assinantes não SQL Server  
 Os seguintes bancos de dados que não são do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são compatíveis como Assinantes com as publicações transacionais e os instantâneos:  
  
-   Oracle para todas as plataformas que o Oracle oferece suporte.  
  
-   IBM DB2 para AS400, MVS, Unix, Linux e Windows.  
  
 Para obter mais informações, consulte [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
  
