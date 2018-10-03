---
title: Desenvolvedor&#39;guia (replicação) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- replication
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server replication]
- programming [SQL Server replication]
- replication [SQL Server], development
ms.assetid: 7ee134ae-1cab-4a35-8017-8ac6d8fc64b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce2054924f26ab5b8d94814c3ad716b00f425064
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212516"
---
# <a name="developer39s-guide-replication"></a>Desenvolvedor&#39;guia (replicação)
  A capacidade de configurar, manter e monitorar programaticamente uma topologia de replicação permite que você simplifique as tarefas de replicação repetidas e aprimore a experiência do usuário em seus aplicativos baseados em replicação. Ao programar a replicação, os seus usuários finais poderão obter funcionalidades de replicação personalizadas sem precisar conhecer os procedimentos armazenados de replicação e os executáveis do agente de replicação ou ter de usar a interface do usuário de replicação implementada por [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 A seguir, cenários nos quais os seus aplicativos poderiam se beneficiar do acesso programático a serviços de replicação:  
  
-   Adição de funcionalidades de replicação a um aplicativo de usuário final existente, como a sincronização de uma assinatura pull quando o usuário clica em um botão.  
  
-   Criação de uma interface do usuário baseada na Web para administração remota da replicação.  
  
-   Criação de uma interface do usuário personalizada que exiba somente um subconjunto da funcionalidade de administração, que pode ser usado para administrar remotamente várias topologias de replicação a partir de um único local, ou que combine as funcionalidades de administração e de sincronização.  
  
-   Aprimoramento de uma ferramenta de monitoramento existente adicionando a capacidade de monitorar o status de uma publicação, assinatura ou no Distribuidor.  
  
-   Criação de um aplicativo personalizado para administrar ou sincronizar assinaturas de um publicador Oracle.  
  
-   Gravação de regras de negócio personalizadas executadas quando uma assinatura de mesclagem for sincronizada.  
  
-   Geração de scripts [!INCLUDE[tsql](../../../includes/tsql-md.md)] que podem ser executados de forma repetida na configuração de Assinantes novos.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que você controle programaticamente os agentes de replicação e administre e monitore programaticamente uma topologia de replicação. Para saber mais sobre como programar a replicação, consulte [Conceitos de programação da replicação](replication-programming-concepts.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Conceitos de programação da replicação](replication-programming-concepts.md)  
 Descreve as etapas de planejamento para desenvolver um aplicativo que use a replicação.  
  
 [Replication System Stored Procedures Concepts](replication-system-stored-procedures-concepts.md)  
 Descreve como os procedimentos armazenados do sistema podem ser usados para oferecem acesso programático em uma topologia de replicação.  
  
 [Conceitos de objetos de gerenciamento de replicação](replication-management-objects-concepts.md)  
 Explica os conceitos da utilização de RMO (Replication Management Objects). Esse é um assembly de código gerenciado que encapsula funcionalidades de replicação para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Conceitos dos executáveis do Agente de Replicação](replication-agent-executables-concepts.md)  
 Descreve o uso dos arquivos executáveis do Replication Agent.  
  
 [Guia do desenvolvedor: Tópicos de instruções &#40;replicação&#41;](../developer-s-guide-how-to-topics-replication.md)  
 Fornece uma lista de tópicos de instruções relacionadas à replicação.  
  
  
