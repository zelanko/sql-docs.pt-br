---
title: MSSQLSERVER_926 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 926 (Database Engine error)
ms.assetid: 57e01668-883b-4be4-84a8-a111caaf0486
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e915f74e6bd3e686916aeb2de2f78d8d2e9ae439
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67937955"
---
# <a name="mssqlserver_926"></a>MSSQLSERVER_926
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
[Fazer backup e restaurar bancos de dados do SQL Server](~/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[sys.sysdatabases &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)  
[Anexar e desanexar bancos de dados &#40;SQL Server&#41;](~/relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
