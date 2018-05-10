---
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
caps.latest.revision: 4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b47c10375c7103e62ba5ae7d833118a3689f73d8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
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
  
