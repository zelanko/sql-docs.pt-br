---
title: MSSQLSERVER_3314 | Microsoft Docs
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
- 3314 (Database Engine error)
ms.assetid: f3a5ca6a-b502-4cab-b3b1-4bc753763fa9
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e60c3345b5e4c7dcb9ab2999bdb5b5f25b22fa4c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3314"></a>MSSQLSERVER_3314
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3314|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ERR_LOG_RID2|  
|Texto da mensagem|Ocorreu um erro na ID do registro de log %S_LSN ao desfazer uma operação registrada no banco de dados '%.*ls'. Em geral, a falha específica é registrada anteriormente como um erro no serviço Log de Eventos do Windows. Repare ou restaure o banco de dados usando um backup.|  
  
## <a name="explanation"></a>Explicação  
Trata-se de um erro de rollup ao desfazer a recuperação. Esse erro colocou o banco de dados no estado SUSPECT. O grupo de arquivos primário, e possivelmente outros grupos de arquivos, estão sob suspeita e podem estar danificados. O banco de dados não pode ser recuperado durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, portanto, não está disponível. Ação do usuário é necessária para resolver o problema.  
  
Observe que, se esse erro ocorrer para **tempdb**, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será desativada.  
  
## <a name="user-action"></a>Ação do usuário  
Este erro pode ser causado por uma condição transitória existente no sistema durante uma determinada tentativa de iniciar a instância de servidor ou recuperar um banco de dados. Este erro também pode ser causado por uma falha permanente que ocorre toda vez que você tenta iniciar o banco de dados. Para obter informações sobre a causa, examine o Log de Eventos do Windows para procurar um erro anterior que indique a falha específica.  
  
Para obter informações sobre a causa dessa ocorrência do erro 3314, examine o Log de Eventos do Windows para procurar um erro anterior que indique a falha específica. A ação do usuário adequada depende de se as informações no Log de Eventos do Windows indicam se o erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi provocado por uma condição transitória ou por uma falha permanente. Para obter informações sobre as ações do usuário para solucionar o erro 3314, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Restaurações completas de banco de dados &#40;modelo de recuperação simples#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
