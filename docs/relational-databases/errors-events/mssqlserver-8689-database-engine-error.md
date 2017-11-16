---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: b087239a8daadf20c15374524b61cbcf7c468b38
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8689|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|USEPLAN_ERR_NO_DB|  
|Texto da mensagem|O banco de dados '%.*ls', especificado na dica USE PLAN, não existe. Especifique um banco de dados existente.|  
  
## <a name="explanation"></a>Explicação  
Um banco de dados especificado na dica USE PLAN não existe.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se todos os bancos de dados que estão especificados na dica USE PLAN existem.  
  
## <a name="see-also"></a>Consulte também  
[Query Hints &#40;Transact-SQL&#41; [Dicas de consulta (Transact-SQL)]](~/t-sql/queries/hints-transact-sql-query.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
  
