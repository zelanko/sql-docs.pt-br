---
title: MSSQLSERVER_9002 | Microsoft Docs
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
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 577160666fc4ec80d75f39ff5a75f05037f3cf8a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver9002"></a>MSSQLSERVER_9002
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9002|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOG_IS_FULL|  
|Texto da mensagem|O log de transações do banco de dados '%.*ls' está cheio. Para saber o motivo pelo qual o espaço no log não pode ser usado novamente, consulte a coluna log_reuse_wait_desc em sys.databases.|  
  
## <a name="explanation"></a>Explicação  
O log de banco de dados não tem espaço. A coluna **log_reuse_wait_desc** em **sys.databases** descreve o motivo pelo qual o espaço no log não pode ser reutilizado.  
  
## <a name="user-action"></a>Ação do usuário  
Use **sys.databases** para determinar por que o log está cheio e, em seguida, corrija a condição. Para obter mais informações, consulte "Solucionando problemas em um log de transação completa (erro 9002)" nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
[Solução de problemas em um log de transação completa &#40;Erro do SQL Server 9002&#41;](~/relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
