---
title: "Validar guias de plano depois da atualiza&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-plan-guides"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "guias de plano [SQL Server], validando após a atualização"
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Validar guias de plano depois da atualiza&#231;&#227;o
  Recomendamos que as definições do guia de plano sejam reavaliadas e testadas quando o aplicativo for atualizado para uma nova versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os requisitos de ajuste de desempenho e o comportamento da correlação do guia de plano podem variar. Embora um guia inválido não cause a falha da consulta, o plano é compilado sem usar o guia de plano e pode não ser a melhor escolha. Depois de atualizar o banco de dados para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], nós recomendamos que as seguintes tarefas sejam executadas:  
  
-   Valide os guias de plano por meio da função [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md).  
  
-   Use eventos estendidos para monitorar os planos mal-encaminhados por algum tempo usando o evento [Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md).  
  
  