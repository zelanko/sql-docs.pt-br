---
title: "Procedimentos armazenados compilados nativamente e opções de execução de set | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 02a1683278d0f64ac41893a9cdb8e97a634002b5
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>Procedimentos armazenados compilados nativamente e opções de execução Set
  As opções de sessão são corrigidas nos blocos atômicos. A execução de um procedimento armazenado não é afetada pelas opções SET de uma sessão. No entanto, determinadas opções SET, como SET NOEXEC e SET SHOWPLAN_XML, fazem com que os procedimentos armazenados (incluindo os procedimentos armazenados compilados nativamente) não sejam executados.  
  
 Quando um procedimento armazenado compilado nativamente for executado com qualquer opção STATISTICS ativada, as estatísticas serão coletadas para o procedimento como um todo, e não por instrução. Para obter mais informações, veja [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md), [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-profile-transact-sql.md), [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md) e [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md). Para obter estatísticas de execução no nível por instrução em procedimentos armazenados criados nativamente, use uma sessão de evento estendido no evento sp_statement_completed, que inicia quando cada consulta individual em uma execução de procedimentos armazenados é concluída. Para obter mais informações sobre como criar sessões de Eventos Estendidos, veja [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).  
  
 Há suporte para **SHOWPLAN_XML** para procedimentos armazenados compilados de modo nativo. Não há suporte para**SHOWPLAN_ALL** e **SHOWPLAN_TEXT** em procedimentos armazenados compilados de modo nativo.  
  
 Não há suporte para**SET FMTONLY** com procedimentos armazenados compilados nativamente. Em vez disso, use [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
