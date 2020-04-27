---
title: MSSQLSERVER_926 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 926 (Database Engine error)
ms.assetid: 57e01668-883b-4be4-84a8-a111caaf0486
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4afdc9adae6f968ca89ff1a9b2bf9e5b67992037
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62912468"
---
# <a name="mssqlserver_926"></a>MSSQLSERVER_926
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|926|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DB_SUSPECT|  
|Texto da mensagem|O banco de dados '%.*ls' não pode ser aberto. Ele foi marcado como SUSPECT pela recuperação. Consulte o log de erros do SQL Server para obter mais informações.|  
  
## <a name="explanation"></a>Explicação  
 O banco de dados foi marcado como suspeito porque houve falha no processo de recuperação que leva um banco de dados a um estado transacional consistente. Isso pode acontecer durante as seguintes operações:  
  
-   Inicializando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Anexando um banco de dados.  
  
-   Usando os procedimentos de RESTORE LOG ou RESTORE para restaurar o banco de dados.  
  
## <a name="user-action"></a>Ação do usuário  
 Inspecione o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e determine a causa do erro. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiver sido reiniciado desde a falha na recuperação, veja os logs de erros anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar a razão pela qual houve falha na recuperação.  
  
 Se a recuperação tiver apresentado falha devido a um erro persistente de E/S, uma página interrompida ou outro possível problema de hardware, resolva o problema de hardware subjacente e restaure o banco de dados usando um backup. Se nenhum backup estiver disponível, considere as opções de reparo de DBCC CHECKDB.  
  
 Se você não conseguir resolver esse problema, entre em contato com o provedor de suporte. Tenha o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponível para revisão.  
  
## <a name="see-also"></a>Consulte Também  
 [Backup e restauração de bancos de dados SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [sys. sysdatabases &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql)   
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
