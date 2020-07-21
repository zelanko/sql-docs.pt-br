---
title: MSSQLSERVER_9002 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4aec35b54d62178ab27b9df007b126e4c05a5a21
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86550769"
---
# <a name="mssqlserver_9002"></a>MSSQLSERVER_9002
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|9002|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOG_IS_FULL|  
|Texto da mensagem|O log de transações do banco de dados '%.*ls' está cheio. Para saber o motivo pelo qual o espaço no log não pode ser usado novamente, consulte a coluna log_reuse_wait_desc em sys.databases.|  
  
## <a name="explanation"></a>Explicação  
 O log de banco de dados não tem espaço. A coluna **log_reuse_wait_desc** em **sys.databases** descreve o motivo pelo qual o espaço no log não pode ser reutilizado.  
  
## <a name="user-action"></a>Ação do usuário  
 Use **sys.databases** para determinar por que o log está cheio e, em seguida, corrija a condição. Para obter mais informações, consulte "Solucionando problemas em um log de transação completa (erro 9002)" nos Manuais Online do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Solução de problemas de um log de transações cheio &#40;Erro 9002 do SQL Server &#41;](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
