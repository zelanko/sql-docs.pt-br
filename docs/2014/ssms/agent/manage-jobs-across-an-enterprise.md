---
title: Gerenciar trabalhos em toda a empresa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f051b3de9ba88354f5fded8cd1f429e3b277747
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188175"
---
# <a name="manage-jobs-across-an-enterprise"></a>Gerenciar trabalhos em toda a empresa
  Se você fizer alterações nas definições de trabalho multisservidor fora [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]do, deverá postar as alterações na lista de download para que os servidores de destino possam baixar o trabalho atualizado novamente. Para garantir que os servidores de destino possuam as definições de trabalho atuais, poste uma instrução INSERT após atualizar o trabalho multisservidor, da seguinte maneira:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 Para notificar servidores de destino de que um trabalho multisservidor foi modificado, é necessário invocar o comando precedente, depois de usar um dos seguintes procedimentos:  
  
-   [sp_add_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_update_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql)  
  
-   [sp_delete_jobstep (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql)  
  
-   [&#41;&#40;Transact-SQL de sp_attach_schedule](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [&#41;&#40;Transact-SQL de sp_detach_schedule](/sql/relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql)  
  
    > [!NOTE]  
    >  Não é necessário chamar **sp_post_msx_operation** depois de chamar **sp_update_job** ou **sp_delete_job**, pois esses procedimentos armazenados postam as alterações requeridas na lista de downloads automaticamente.  
  
 As seguintes tarefas são comuns no gerenciamento de trabalhos em toda a empresa:  
  
 **Para verificar o status de um servidor de destino**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)  
  
-   [SQL Server Management Objects (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **Para alterar os servidores de destino de um trabalho**  
  
-   [SQL Server Management Studio](modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
-   [SQL Server Management Objects (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **Para alterar o local de um servidor de destino**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
-   [SQL Server Management Objects (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **Para sincronizar os relógios do servidor de destino**  
  
-   [SQL Server Management Studio](synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)  
  
 **Para forçar um servidor de destino a sondar o servidor mestre**  
  
-   [SQL Server Management Studio](force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar eventos](manage-events.md)  
  
  
