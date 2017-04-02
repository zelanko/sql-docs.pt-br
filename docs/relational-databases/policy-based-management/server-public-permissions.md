---
title: "Permiss&#245;es p&#250;blicas de servidor | Microsoft Docs"
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
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Permiss&#245;es p&#250;blicas de servidor
  Esta regra determina se a função de servidor público tem permissões de servidor. Todo logon criado no servidor é um membro da função de servidor público. Se esta condição for atendida, todo logon no servidor terá permissões de servidor.  
  
## Práticas Recomendadas  
 Não conceda permissões de servidor à função de servidor público.  
  
> [!IMPORTANT]  
>  Depois que a instalação for concluída, a função **PUBLIC** terá a permissão **CONNECT** em todos os pontos de extremidade, exceto em **Conexão de Administrador Dedicada**. Isso é normal e não deve ser alterado. (O acesso é controlado pela permissão **CONNECT SQL**, que é concedida automaticamente quando novos logons são criados.)  
  
### Para obter mais informações  
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
  