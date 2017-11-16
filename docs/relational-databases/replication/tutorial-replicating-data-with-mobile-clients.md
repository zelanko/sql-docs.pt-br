---
title: "Tutorial: replicando dados com clientes móveis | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
helpviewer_keywords: replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 642f2fa95b2ff69f11a10f7bbaae6e184928c7b9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>Tutorial: Replicando dados com clientes móveis
A replicação é uma boa solução para o problema de mover dados entre um servidor central e clientes móveis que são conectados apenas ocasionalmente. Usando os assistentes de replicação, você pode configurar e administrar uma topologia de replicação facilmente. Este tutorial mostra como você deve configurar uma topologia de replicação para clientes móveis.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
Neste tutorial você usará a replicação de mesclagem para publicar dados de um banco de dados central para um ou mais usuários móveis de forma que cada usuário obtenha um subconjunto dos dados filtrado exclusivamente. A primeira lição mostra como usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar uma publicação. Lições posteriores mostram como criar e sincronizar uma assinatura.  
  
## <a name="requirements"></a>Requisitos  
Este tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que possuem pouca experiência com replicação. Antes de iniciar este tutorial, é necessário concluir o [Tutorial: Preparando o servidor para replicação](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para que você possa usar esse tutorial, os seguintes componentes devem estar instalados no sistema:  
  
-   No servidor do Publicador (fonte):  
  
    -   Qualquer edição do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], menos a Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) ou [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Essas edições não podem ser Publicadores de replicação.  
  
    -   O banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
-   Servidor de assinante (destino):  
  
    -   Qualquer edição do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], exceto para [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
    > [!NOTE]  
    > A replicação não é instalada por padrão no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
> [!NOTE]  
> No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve se conectar ao Publicador e ao Assinante usando um logon que seja membro da função de servidor fixa sysadmin.  
  
**Tempo estimado para concluir este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial  
  
-   [Lição 1: Publicando dados usando replicação de mesclagem](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
-   [Lição 2: Criando uma assinatura na publicação de mesclagem](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
[Inicie o tutorial](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
## <a name="see-also"></a>Consulte também  
[Conceitos de programação de replicação](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  
