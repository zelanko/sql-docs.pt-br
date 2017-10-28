---
title: "Tutorial: replicando dados entre servidores que estão continuamente conectados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6090a59e8f831d5d05def6f6ff65ee99a09aea84
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-replicating-data-between-continuously-connected-servers"></a>Tutorial: Replicando dados entre servidores que estão continuamente conectados
Replicação é uma boa solução ao problema de mover dados entre servidores que estão continuamente conectados. Usando os assistentes de replicação, você pode configurar e administrar uma topologia de replicação facilmente. Este tutorial mostra a você como configurar uma topologia de replicação para servidores continuamente conectados.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Este tutorial mostrará a você como publicar dados de um banco de dados para outro usando replicação transacional. A primeira lição mostra como usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar uma publicação. Depois, as lições mostrarão como criar e validar uma assinatura e como medir a latência.  
  
## <a name="requirements"></a>Requisitos  
Este tutorial é destinado a usuários que estão familiarizados com operações básicas de banco de dados, mas que possuem pouca experiência com replicação. Este tutorial exige a conclusão do tutorial anterior, [Preparando o servidor para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para usar este tutorial, os seguintes componentes devem fazer parte do seu sistema:  
  
-   No servidor do Publicador (fonte):  
  
    -   Qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], menos a Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) ou [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Estas edições não podem ser Publicadores de replicação.  
  
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] banco de dados de exemplo. Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
-   Servidor de assinante (destino):  
  
    -   Qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exceto [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] não pode ser um Assinante em uma replicação transacional.  
  
    > [!NOTE]  
    > A replicação não é instalada por padrão no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .  
  
> [!NOTE]  
> No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve se conectar ao Publicador e ao Assinante usando um logon que seja membro da função de servidor fixa **sysadmin** .  
  
**Tempo estimado para concluir este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial  
  
-   [Lição 1: publicando dados que usam replicação transacional](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
-   [Lição 2: Criando uma assinatura na publicação transacional](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md)  
  
-   [Lição 3: Validando a assinatura e medindo a latência](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md)  
  
[Inicie o tutorial](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
## <a name="see-also"></a>Consulte também  
[Conceitos de programação de replicação](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  

