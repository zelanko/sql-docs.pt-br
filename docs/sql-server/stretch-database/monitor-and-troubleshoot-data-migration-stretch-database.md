---
title: "Monitorar e solucionar problemas de migração de dados (Stretch Database) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 91c10b51a3fec9ccc96c3aa23100abdf2a60ba81
ms.lasthandoff: 04/11/2017

---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>Monitorar e solucionar problemas de migração de dados (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para monitorar a migração de dados no Monitor do Stretch Database, selecione **Tarefas | Stretch | Monitorar** para um banco de dados no SQL Server Management Studio.  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Verificar o status de migração de dados no monitor do Stretch Database  
 Selecione **Tarefas | Stretch | Monitorar** para que um banco de dados no SQL Server Management Studio abra o monitor do Stretch Database e monitore a migração de dados.  
  
-   A parte superior do monitor exibe informações gerais sobre o banco de dados SQL Server habilitado para Stretch e o banco de dados remoto do Azure.  
  
-   A parte inferior do monitor exibe o status de migração de dados para cada tabela habilitada para o Stretch no banco de dados.  
  
 ![Monitor do Stretch Database](../../sql-server/stretch-database/media/stretch-monitor.PNG "Monitor do Stretch Database")  
  
##  <a name="Migration"></a> Verifique o status da migração de dados em uma exibição de gerenciamento dinâmico  
 Abra a exibição de gerenciamento dinâmico **sys.dm_db_rda_migration_status** para ver quantos lotes e linhas de dados foram migradas. Para obter mais informações, consulte [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
##  <a name="Firewall"></a> Solucionar problemas de migração de dados  
 **Linhas de minha tabela habilitada para o Stretch não estão sendo migradas para o Azure. Qual é o problema?**  
 Há vários problemas que podem afetar a migração. Verifique o seguinte.  
  
-   Verifique a conectividade de rede para o computador do SQL Server.  
  
-   Verifique se o firewall do Azure não está bloqueando o SQL Server de se conectar ao ponto de extremidade remoto.  
  
-   Verifique a exibição do gerenciamento dinâmico **sys.dm_db_rda_migration_status** o status do lote mais recente. Se tiver ocorrido um erro, verifique os valores error_number, error_state e error_severity para o lote.  
  
    -   Para obter mais informações sobre a exibição, consulte [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
    -   Para obter mais informações sobre o conteúdo de uma mensagem de erro do SQL Server, consulte [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md).  
  
 **O firewall do Azure está bloqueando conexões do meu servidor local.**  
 Você precisará adicionar uma regra nas configurações do firewall do Azure do servidor do Azure para permitir que o SQL Server se comunique com o servidor remoto do Azure.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar e solucionar problemas no Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  

