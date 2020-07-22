---
title: Documentação do desenvolvedor de replicação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server replication]
- programming [SQL Server replication]
- replication [SQL Server], development
ms.assetid: 7ee134ae-1cab-4a35-8017-8ac6d8fc64b6
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 950723affaeb6c1e06f16d07967b8fea5adfca75
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914202"
---
# <a name="replication-developer-documentation"></a>Documentação do desenvolvedor de replicação
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]

  A capacidade de configurar, manter e monitorar programaticamente uma topologia de replicação permite que você simplifique as tarefas de replicação repetidas e aprimore a experiência do usuário em seus aplicativos baseados em replicação. Ao programar a replicação, os seus usuários finais poderão obter funcionalidades de replicação personalizadas sem precisar conhecer os procedimentos armazenados de replicação e os executáveis do agente de replicação ou ter de usar a interface do usuário de replicação implementada por [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 A seguir, cenários nos quais os seus aplicativos poderiam se beneficiar do acesso programático a serviços de replicação:  
  
-   Adição de funcionalidades de replicação a um aplicativo de usuário final existente, como a sincronização de uma assinatura pull quando o usuário clica em um botão.  
  
-   Criação de uma interface do usuário baseada na Web para administração remota da replicação.  
  
-   Criação de uma interface do usuário personalizada que exiba somente um subconjunto da funcionalidade de administração, que pode ser usado para administrar remotamente várias topologias de replicação a partir de um único local, ou que combine as funcionalidades de administração e de sincronização.  
  
-   Aprimoramento de uma ferramenta de monitoramento existente adicionando a capacidade de monitorar o status de uma publicação, assinatura ou no Distribuidor.  
  
-   Criação de um aplicativo personalizado para administrar ou sincronizar assinaturas de um publicador Oracle.  
  
-   Gravação de regras de negócio personalizadas executadas quando uma assinatura de mesclagem for sincronizada.  
  
-   Geração de scripts [!INCLUDE[tsql](../../../includes/tsql-md.md)] que podem ser executados de forma repetida na configuração de Assinantes novos.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que você controle programaticamente os agentes de replicação e administre e monitore programaticamente uma topologia de replicação. Para saber mais sobre como programar a replicação, consulte [Conceitos de programação da replicação](../../../relational-databases/replication/concepts/replication-programming-concepts.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Conceitos de programação da replicação](../../../relational-databases/replication/concepts/replication-programming-concepts.md)  
 Descreve as etapas de planejamento para desenvolver um aplicativo que use a replicação.  
  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
 Descreve como os procedimentos armazenados do sistema podem ser usados para oferecem acesso programático em uma topologia de replicação.  
  
 [Conceitos de objetos de gerenciamento de replicação](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
 Explica os conceitos da utilização de RMO (Replication Management Objects). Esse é um assembly de código gerenciado que encapsula funcionalidades de replicação para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
 Descreve o uso dos arquivos executáveis do Replication Agent.  
  
  
  
