---
title: "Monitorando os logs de erros | Microsoft Docs"
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
  - "logs [SQL Server]"
  - "desempenho do banco de dados [SQL Server], erros"
  - "Logs do aplicativo do Windows [SQL Server]"
  - "monitorando o desempenho [SQL Server], erros"
  - "desempenho do servidor [SQL Server], erros"
  - "comparando a saída do log de erros e do aplicativo"
  - "erros [SQL Server], logs"
  - "ajustando bancos de dados [SQL Server], erros"
  - "monitoramento de banco de dados [SQL Server], erros"
  - "log de erros do SQL Server"
  - "logs [SQL Server], logs de erros do SQL Server"
  - "logs de erros [SQL Server]"
  - "logs [SQL Server], logs dos aplicativos do Windows "
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Monitorando os logs de erros
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra determinados eventos de sistema e eventos definidos pelo usuário no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no log do aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Ambos os logs registram automaticamente todos os eventos com carimbos de hora. Use as informações do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para solucionar problemas relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O log do aplicativo do Windows fornece um panorama dos eventos que ocorrem no sistema operacional Windows, bem como dos eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Use o Visualizador de Eventos do Windows para exibir o log do aplicativo e para filtrar as informações. Por exemplo, você pode filtrar eventos, como informações, advertência, erro, auditoria com êxito ou sem êxito.  
  
## Comparando a saída do log de erros e do aplicativo  
 Você pode usar o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o log do aplicativo do Windows para identificar a causa dos problemas. Por exemplo, enquanto monitora o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode encontrar mensagens de erro que não contêm as informações do ocorrido. Comparando as datas e as horas dos eventos entre esses logs, você pode reduzir a lista de causas prováveis. O Visualizador do Arquivo de Log do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] permite integrar os logs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e do Windows à uma única lista, simplificando a compreensão dos eventos relativos ao servidor e aos eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte o tópico "Visualizador do Arquivo de Log" nos Manuais Online do SQL Server.  
  
## Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Exibindo o log de erros do SQL Server](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|Contém informações sobre o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como exibi-lo.|  
|[Exibindo o log do aplicativo do Windows](../../tools/configuration-manager/viewing-the-windows-application-log.md)|Contém informações sobre o log do aplicativo do Windows e como exibi-lo.|  
  
  