---
title: "Categoria de eventos Bloqueios | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Categoria de eventos Bloqueios [SQL Server]"
  - "classes de evento do SQL Server, categoria de evento Locks"
  - "classes de evento [SQL Server], categoria de evento Locks"
  - "escalonamento de bloqueios [SQL Server], categoria de eventos locks"
ms.assetid: 27d6afa2-7dab-4fe7-a1ad-064b879dc654
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Categoria de eventos Bloqueios
  Use as classes de evento na categoria de evento **Locks** para monitorar a atividade de bloqueio em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Essas classes de evento podem ajudar a descobrir problemas de bloqueio causados por vários usuários lendo e modificando dados simultaneamente.  
  
 Como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] frequentemente processa muitos bloqueios, captar as classes de evento **Locks** durante um rastreamento pode incorrer em sobrecarga significativa e resultar em arquivos ou tabelas de rastreamento maiores.  
  
## Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Classe de evento Deadlock Graph](../../relational-databases/event-classes/deadlock-graph-event-class.md)|Fornece uma descrição XML de um deadlock.|  
|[Classe de evento Lock:Acquired](../../relational-databases/event-classes/lock-acquired-event-class.md)|Indica que um bloqueio foi adquirido em um recurso, como uma linha em uma tabela.|  
|[Classe de evento Lock:Cancel](../../relational-databases/event-classes/lock-cancel-event-class.md)|Rastreia solicitações de bloqueios canceladas antes que o bloqueio fosse adquirido (por exemplo, para impedir um deadlock).|  
|[Classe de evento Lock:Deadlock Chain](../../relational-databases/event-classes/lock-deadlock-chain-event-class.md)|Monitora quando ocorrem condições de deadlock e quais objetos são envolvidos.|  
|[Classe de evento Lock:Deadlock](../../relational-databases/event-classes/lock-deadlock-event-class.md)|Rastreia quando uma transação solicitou um bloqueio em um recurso já bloqueado por outra transação, resultando em um deadlock.|  
|[Classe de evento Lock:Escalation](../../relational-databases/event-classes/lock-escalation-event-class.md)|Indica se um bloqueio mais refinado foi convertido em um bloqueio mais rústico.|  
|[Classe de evento Lock:Released](../../relational-databases/event-classes/lock-released-event-class.md)|Rastreia quando um bloqueio é liberado.|  
|[Classe de evento Lock:Timeout &#40;timeout &#62; 0&#41;](../../relational-databases/event-classes/lock-timeout-timeout-0-event-class.md)|Rastreia quando solicitações de bloqueio não podem ser concluídas porque outra transação tem um bloqueio no recurso solicitado. Esse evento só acontece em situações em que o valor de tempo limite de bloqueio é maior que zero.|  
|[Classe de evento Lock:Timeout](../../relational-databases/event-classes/lock-timeout-event-class.md)|Rastreia quando solicitações de bloqueio não podem ser concluídas porque outra transação tem um bloqueio no recurso solicitado.|  
  
  