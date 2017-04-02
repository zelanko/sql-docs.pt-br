---
title: "Usando o Database Mail em vez do SQL Mail | Microsoft Docs"
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
  - "Práticas recomendadas [Mecanismo de Banco de Dados]"
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Usando o Database Mail em vez do SQL Mail
  Esta regra verifica a exibição do catálogo sys.configurations para determinar se a opção de configuração do servidor do SQL Mail XPs está definida como ON.  
  
## Práticas Recomendadas  
 O SQL Mail será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Para enviar email, use o Database Mail.  
  
 O SQL Mail é executado em processo de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o SQL Mail ficar inoperante, o servidor também ficará. O Database Mail é executado fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um processo separado, é escalável e não requer a instalação de componentes de cliente MAPI estendido no servidor de produção.  
  
## Para obter mais informações  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
## Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  