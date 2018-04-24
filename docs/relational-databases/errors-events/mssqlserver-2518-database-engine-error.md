---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2630ce49e02bcb9d1dd3c36914727e3097c5b2de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2518|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|Texto da mensagem|ID de Objeto O_ID (objeto "O_NAME"): colunas computadas e tipos definidos pelo usuário não podem ser verificados quanto a este objeto porque o Common Language Runtime (CLR) está desabilitado.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem informativa indica que o processador de consultas não pôde fornecer para DBCC um objeto interno que permita a avaliação de colunas computadas e de tipos CLR definidos pelo usuário. Esse problema ocorreu porque uma das colunas envolvia o CLR, mas ele não está habilitado. O objeto interno abrange todas as colunas. Por isso, a incapacidade de avaliar uma única coluna impede a criação do objeto interno. Isso significa que as colunas computadas não serão verificadas quanto à correção ou que não serão usadas quando DBCC verificar a consistência entre índices e tabelas base.  
  
## <a name="user-action"></a>Ação do usuário  
Habilite o CLR e execute a instrução DBCC novamente.  
  
## <a name="see-also"></a>Consulte Também  
[Habilitando a integração CLR](~/relational-databases/clr-integration/clr-integration-enabling.md)  
  
