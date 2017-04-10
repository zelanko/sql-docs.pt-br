---
title: "Permiss&#245;es de convidado em bancos de dados de usu&#225;rios | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Práticas recomendadas [Mecanismo de Banco de Dados]"
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Permiss&#245;es de convidado em bancos de dados de usu&#225;rios
  Esta regra determina se o usuário convidado tem permissão para acessar o banco de dados. Esta regra só se aplica a bancos de dados de usuários.  
  
## Práticas Recomendadas  
 Revogue a permissão de usuário convidado para acessar o banco de dados se não for necessária.  
  
 O usuário convidado não pode ser descartado, mas pode ser desabilitado revogando sua permissão CONNECT com a execução de REVOKE CONNECT FROM GUEST em qualquer banco de dados que não seja mestre, tempdb ou msdb.  
  
## Para obter mais informações  
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
## Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  