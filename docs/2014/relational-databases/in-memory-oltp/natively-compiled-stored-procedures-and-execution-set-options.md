---
title: Procedimentos armazenados compilados nativamente e opções de execução de set | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 264a2b3ab1e6f3f0bda97bfe89a4438aa641577d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025853"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>Procedimentos armazenados compilados nativamente e opções de execução Set
  As opções de sessão são corrigidas nos blocos atômicos. A execução de um procedimento armazenado não é afetada pelas opções SET de uma sessão. No entanto, determinadas opções SET, como SET NOEXEC e SET SHOWPLAN_XML, fazem com que os procedimentos armazenados (incluindo os procedimentos armazenados compilados nativamente) não sejam executados.  
  
 Quando um procedimento armazenado compilado nativamente for executado com qualquer opção STATISTICS ativada, as estatísticas serão coletadas para o procedimento como um todo, e não por instrução. Para obter mais informações, veja [SET STATISTICS IO &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-io-transact-sql), [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-profile-transact-sql), [SET STATISTICS TIME &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-time-transact-sql) e [SET STATISTICS XML &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-xml-transact-sql). Para obter estatísticas de execução no nível por instrução em procedimentos armazenados criados nativamente, use uma sessão de evento estendido no evento sp_statement_completed, que inicia quando cada consulta individual em uma execução de procedimentos armazenados é concluída. Para obter mais informações sobre como criar sessões de Eventos Estendidos, veja [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql).  
  
 Há suporte para o `SHOWPLAN_XML` para procedimentos armazenados compilados nativamente. Não há suporte para `SHOWPLAN_ALL` e `SHOWPLAN_TEXT` com procedimentos armazenados compilados nativamente.  
  
 Não há suporte para `SET FMTONLY` com procedimentos armazenados compilados nativamente. Em vez disso, use [sp_describe_first_result_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)  
  
  
