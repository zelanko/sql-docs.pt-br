---
title: MSSQLSERVER_12304 | Microsoft Docs
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
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
caps.latest.revision: 4
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93b4beb33bb58f9e0e5c87fcd7b02f515fbd6fff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver12304"></a>MSSQLSERVER_12304
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|12304|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|Texto da mensagem|Usar um tipo de tabela com otimização de memória que usa a propriedade IDENTITY com qualquer uma de suas colunas não tem suporte ao usar o tipo fora do contexto de um procedimento armazenado compilado nativamente.|  
  
## <a name="user-action"></a>Ação do usuário  
Não use um tipo de tabela com otimização de memória que usa a propriedade de identidade com qualquer uma de suas colunas.  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
