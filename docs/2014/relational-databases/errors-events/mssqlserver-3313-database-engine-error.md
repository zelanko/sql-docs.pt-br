---
title: MSSQLSERVER_3313 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 3313 (Database Engine error)
ms.assetid: a244227b-8553-42df-9435-034f906c4c74
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 695e747a5b5e9f676c123e946f30824556107e7b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408455"
---
# <a name="mssqlserver3313"></a>MSSQLSERVER_3313
    
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
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
