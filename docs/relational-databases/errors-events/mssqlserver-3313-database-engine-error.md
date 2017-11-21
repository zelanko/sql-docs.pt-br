---
title: MSSQLSERVER_3313 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3313 (Database Engine error)
ms.assetid: a244227b-8553-42df-9435-034f906c4c74
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6e8b07b5a12de6b011ee581e0d869c4ec30427e3
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3313"></a>MSSQLSERVER_3313
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3313|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ERR_LOG_RID1|  
|Texto da mensagem|Ocorreu um erro na ID do registro de log %S_LSN ao refazer uma operação registrada no banco de dados '%.*ls'. Em geral, a falha específica é registrada anteriormente como um erro no serviço Log de Eventos do Windows. Repare ou restaure o banco de dados usando um backup completo.|  
  
## <a name="explanation"></a>Explicação  
Trata-se de um erro de rollup ao refazer uma recuperação. Esse erro colocou o banco de dados no estado SUSPECT. O grupo de arquivos primário, e possivelmente outros grupos de arquivos, estão sob suspeita e podem estar danificados. O banco de dados não pode ser recuperado durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, portanto, não está disponível. Ação do usuário é necessária para resolver o problema.  
  
Observe que, se esse erro ocorrer para **tempdb**, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será desativada.  
  
## <a name="user-action"></a>Ação do usuário  
Este erro pode ser causado por uma condição transitória existente no sistema durante uma determinada tentativa de iniciar a instância de servidor ou recuperar um banco de dados. Este erro também pode ser causado por uma falha permanente que ocorre toda vez que você tenta iniciar o banco de dados. Para obter informações sobre a causa, examine o Log de Eventos do Windows para procurar um erro anterior que indique a falha específica.  
  
Observe que, quando essa condição de erro é encontrada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente gera três arquivos na pasta **LOG** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O arquivo SQLDump*nnnn*.txt contém informações de diagnóstico avançadas referentes às falhas, incluindo os detalhes sobre a transação e a página que tiveram o problema. Estas informações são usadas normalmente pela equipe de Suporte de Produto para analisar a razão para a falha.  
  
Para obter informações sobre a causa dessa ocorrência do erro 3313, examine o Log de Eventos do Windows para obter um erro anterior que indica a falha específica. A ação do usuário adequada depende de se as informações no Log de Eventos do Windows indicam se o erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi provocado por uma condição transitória ou por uma falha permanente. Para obter informações sobre as ações do usuário para solucionar o erro 3313, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Restaurações completas de banco de dados &#40;modelo de recuperação simples#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  

