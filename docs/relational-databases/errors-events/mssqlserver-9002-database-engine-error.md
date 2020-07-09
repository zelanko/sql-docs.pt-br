---
title: MSSQLSERVER_9002 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6e888a44cd96eeaa93f49c02128e48763b66a9ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85636635"
---
# <a name="mssqlserver_9002"></a>MSSQLSERVER_9002
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
[Solução de problemas de um log de transação completa &#40;Erro do SQL Server 9002&#41;](~/relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
