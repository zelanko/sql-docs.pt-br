---
title: 'Tutorial: replicando dados com clientes móveis | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b8c9e2d0f20a91bb11c0d5e08aff00c27785818e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85047590"
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>Tutorial: Replicando dados com clientes móveis
  A replicação é uma boa solução para o problema de mover dados entre um servidor central e clientes móveis que são conectados apenas ocasionalmente. Usando os assistentes de replicação, você pode configurar e administrar uma topologia de replicação facilmente. Este tutorial mostra como você deve configurar uma topologia de replicação para clientes móveis.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Neste tutorial você usará a replicação de mesclagem para publicar dados de um banco de dados central para um ou mais usuários móveis de forma que cada usuário obtenha um subconjunto dos dados filtrado exclusivamente. A primeira lição mostra como usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar uma publicação. Lições posteriores mostram como criar e sincronizar uma assinatura.  
  
## <a name="requirements"></a>Requisitos  
 Este tutorial é destinado a usuários que estão familiarizados com operações fundamentais de bancos de dados, mas que possuem pouca experiência com replicação. Antes de iniciar este tutorial, você deve concluir [o tutorial: preparando o servidor para replicação](tutorial-preparing-the-server-for-replication.md).  
  
 Para que você possa usar esse tutorial, os seguintes componentes devem estar instalados no sistema:  
  
-   No servidor do Publicador (fonte):  
  
    -   Qualquer edição do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], menos a Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) ou [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Essas edições não podem ser Publicadores de replicação.  
  
    -   O banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão.  
  
-   Servidor de assinante (destino):  
  
    -   Qualquer edição do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], exceto para [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
    > [!NOTE]  
    >  A replicação não é instalada por padrão no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
> [!NOTE]  
>  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você deve se conectar ao Publicador e ao Assinante usando um logon que seja membro da função de servidor fixa sysadmin.  
  
 **Tempo estimado para concluir este tutorial: 30 minutos.**  
  
## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial  
  
-   [Lição 1: publicando dados usando a replicação de mesclagem](lesson-1-publishing-data-using-merge-replication.md)  
  
-   [Lição 2: criando uma assinatura para a publicação de mesclagem](lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
 [Iniciar o tutorial](merge/merge-replication.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de programação de replicação](concepts/replication-programming-concepts.md)  
  
  
