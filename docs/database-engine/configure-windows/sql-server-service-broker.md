---
title: SQL Server Service Broker | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL13.SWB.SSBMSGTYPEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBCONTRACTPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBQUEUEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBREMSVCBINDPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBROUTEPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBPRIORITYPROPERTIES.GENERAL.F1
- SQL13.SWB.SSBSERVICEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- Broker See Service Broker
- SQL Server Service Broker
- Service Broker
ms.assetid: 8b8b3b57-fd46-44de-9a4e-e3a8e3999c1e
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: fab7b17dd546ed4723df73d3ee166e125090b57d
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="sql-server-service-broker"></a>SQL Server Service Broker
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] oferece suporte nativo para aplicativos de mensagens e enfileiramento no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Isso facilita para os desenvolvedores a criação de aplicativos sofisticados que usam os componentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para comunicação entre bancos de dados díspares. Os desenvolvedores podem usar o [!INCLUDE[ssSB](../../includes/sssb-md.md)] para criar facilmente aplicativos distribuídos e confiáveis.  
  
 Os desenvolvedores de aplicativos que usam o [!INCLUDE[ssSB](../../includes/sssb-md.md)] podem distribuir cargas de trabalho de dados por vários bancos de dados sem programação de comunicação complexa e mensagens internas. Isso reduz o trabalho de desenvolvimento e teste porque o [!INCLUDE[ssSB](../../includes/sssb-md.md)] controla os caminhos de comunicação no contexto de uma conversa. Isso também melhora o desempenho. Por exemplo, bancos de dados front-end que oferecem suporte a sites podem gravar informações e enviar tarefas intensivas de processamento para enfileiramento em bancos de dados back-end. [!INCLUDE[ssSB](../../includes/sssb-md.md)] garante que todas as tarefas sejam gerenciadas no contexto de transações para assegurar a confiabilidade e a consistência técnica.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]
  
## <a name="where-is-the-documentation-for-service-broker"></a>Onde está a documentação do Service Broker?  
 A documentação de referência do [!INCLUDE[ssSB](../../includes/sssb-md.md)] está incluída na documentação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Esta documentação de referência inclui as seguintes seções:  
  
-   [Instruções DDL &#40;Linguagem de Definição de Dados&#41; &#40;Transact-SQL&#41;](~/mdx/mdx-data-definition-statements-mdx.md) para instruções CREATE, ALTER e DROP  
  
-   [Instruções do Service Broker](../../t-sql/statements/service-broker-statements.md)  
  
-   [Exibições de catálogo do Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)  
  
-   [Exibições de gerenciamento dinâmico relacionadas ao Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
-   [Utilitário ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
 Consulte a [documentação publicada anteriormente](http://go.microsoft.com/fwlink/?LinkId=231312) para saber mais sobre conceitos do [!INCLUDE[ssSB](../../includes/sssb-md.md)] e sobre tarefas de desenvolvimento e gerenciamento. Esta documentação não é reproduzida na documentação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] devido ao pequeno número de alterações no [!INCLUDE[ssSB](../../includes/sssb-md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="whats-new-in-service-broker"></a>Novidades no Service Broker  
 Nenhuma alteração significativa foi introduzida no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  As alterações a seguir foram introduzidas no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
### <a name="messages-can-be-sent-to-multiple-target-services-multicast"></a>As mensagens podem ser enviadas a vários serviços de destino (multicast)  
 A sintaxe da instrução [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md) foi estendida para habilitar o multicast, dando suporte a vários identificadores de conversa.  
  
### <a name="queues-expose-the-message-enqueued-time"></a>Filas expõem o tempo de enfileiramento da mensagem  
 Filas têm uma nova coluna, **message_enqueue_time**, que mostra quanto tempo uma mensagem permaneceu na fila.  
  
### <a name="poison-message-handling-can-be-disabled"></a>A manipulação de mensagens suspeitas pode estar desabilitada  
 As instruções [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md) e [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md) agora tem a capacidade de habilitar ou desabilitar a manipulação de mensagens suspeitas adicionando a cláusula `POISON_MESSAGE_HANDLING (STATUS = ON | OFF)`. A exibição de catálogo **sys.service_queues** agora tem a coluna **is_poison_message_handling_enabled** para indicar se a mensagem suspeita está habilitada ou desabilitada.  
  
### <a name="always-on-support-in-service-broker"></a>Suporte AlwaysOn no Service Broker  
 Para obter mais informações, consulte [Service Broker com Grupos de Disponibilidade AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/service-broker-with-always-on-availability-groups-sql-server.md).  
  
  

