---
title: MSSQLSERVER_3414 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 890179c3f5a6bc7d3d627ce9cf2c51fc5d2e96ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868271"
---
# <a name="mssqlserver3414"></a>MSSQLSERVER_3414
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3414|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REC_GIVEUP|  
|Texto da mensagem|Erro durante a recuperação, o que impede a reinicialização do banco de dados '%.*ls' (ID do banco de dados %d). Diagnostique os erros de recuperação e corrija-os ou restaure usando um backup válido. Se os erros não forem corrigidos ou se não eram esperados, entre em contato com o Suporte Técnico.|  
  
## <a name="explanation"></a>Explicação  
 O banco de dados especificado foi recuperado, mas não foi iniciado, porque aconteceram erros durante a recuperação. Esse erro colocou o banco de dados no estado SUSPECT. O grupo de arquivos primário, e possivelmente outros grupos de arquivos, estão sob suspeita e podem estar danificados. O banco de dados não pode ser recuperado durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, portanto, não está disponível. Ação do usuário é necessária para resolver o problema.  
  
 Observe que, se esse erro ocorrer para **tempdb**, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será desativada.  
  
## <a name="user-action"></a>Ação do usuário  
 Este erro pode ser causado por uma condição transitória existente no sistema durante uma determinada tentativa de iniciar a instância de servidor ou recuperar um banco de dados. Este erro também pode ser causado por uma falha permanente que ocorre toda vez que você tenta iniciar o banco de dados. Para obter informações sobre a causa, examine o Log de Eventos do Windows para procurar um erro anterior que indique a falha específica.  
  
 Para obter informações sobre a causa dessa ocorrência do erro 3414, examine o Log de Eventos do Windows para procurar um erro anterior que indique a falha específica. A ação do usuário adequada depende de se as informações no Log de Eventos do Windows indicam se o erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi provocado por uma condição transitória ou por uma falha permanente. Para obter informações sobre as ações do usuário para solucionar o erro 3414, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [Restaurações completas de banco de dados &#40;Modelo de recuperação simples#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
