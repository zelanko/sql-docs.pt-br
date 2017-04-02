---
title: "O estado de sincroniza&#231;&#227;o de dados do banco de dados de disponibilidade n&#227;o &#233; &#237;ntegro | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.agdashboard.arp3datasynchealthy.issues.f1"
helpviewer_keywords: 
  - "Grupos de disponibilidade [SQL Server], políticas"
ms.assetid: 4fd003e7-808e-4b0e-b28a-47d9f2616f06
caps.latest.revision: 15
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "erikre"
caps.handback.revision: 15
---
# O estado de sincroniza&#231;&#227;o de dados do banco de dados de disponibilidade n&#227;o &#233; &#237;ntegro
    
## Introdução  
  
|||  
|-|-|  
|**Nome da Política**|Estado de Sincronização dos Dados do Banco de Dados de Disponibilidade|  
|**Problema**|O estado de sincronização de dados do banco de dados de disponibilidade não é íntegro.|  
|**Categoria**|**Aviso**|  
|**Faceta**|Banco de dados de disponibilidade|  
  
## Descrição  
 Esta política acumula o estado de sincronização de dados de todos os bancos de dados de disponibilidade (também chamados de "réplicas de banco de dados") na réplica de disponibilidade. A política estará em estado não íntegro quando alguma réplica de banco de dados não estiver no estado de sincronização de dados esperado. Caso contrário, a política estará em um estado íntegro.  
  
> [!NOTE]  
>  Para esta versão do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], as informações sobre possíveis causas e soluções estão localizadas em [O estado de sincronização de dados de algum banco de dados de disponibilidade não é íntegro](http://go.microsoft.com/fwlink/p/?LinkId=220858) no TechNet Wiki.  
  
## Causas possíveis  
 O estado de sincronização de dados deste banco de dados de disponibilidade não é íntegro. Em uma réplica de disponibilidade de confirmação de transação, todos os bancos de dados de disponibilidade devem estar no estado SYNCHRONIZING. Em uma réplica de disponibilidade da confirmação síncrona, todo banco de dados de disponibilidade deve estar no estado SYNCHRONIZING.  
  
## Solução possível  
 Use a política de réplica de banco de dados para localizar a réplica de banco de dados em estado de sincronização de dados não íntegro e depois resolva o problema na réplica de banco de dados.  
  
## Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../Topic/Overview%20of%20Always On%20Availability%20Groups%20\(SQL%20Server\).md)   
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../Topic/Use%20the%20Always On%20Dashboard%20\(SQL%20Server%20Management%20Studio\).md)  
  
  