---
title: "Definir a op&#231;&#227;o do banco de dados AUTO_CLOSE como OFF | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Práticas recomendadas [Mecanismo de Banco de Dados]"
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Definir a op&#231;&#227;o do banco de dados AUTO_CLOSE como OFF
  Esta regra verifica se a opção AUTO_ CLOSE é definida como OFF. Quando a opção AUTO_CLOSE está definido como ON, pode causar degradação do desempenho em bancos de dados acessados com frequência, por causa do aumento da sobrecarga ao abrir e fechar o banco de dados após cada conexão. AUTO_CLOSE também libera o cache de procedimento depois de cada conexão.  
  
## Práticas Recomendadas  
 Se um banco de dados for acessado frequentemente, defina sua opção de AUTO_CLOSE como OFF.  
  
## Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)  
  
## Consulte também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  