---
title: Gerenciar trabalhos em toda a empresa
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b4eb4810d62a1ba669803997432c00ae4539e7db
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726982"
---
# <a name="manage-jobs-across-an-enterprise"></a>Gerenciar trabalhos em toda a empresa
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Se você fizer alterações em definições de trabalho multisservidor fora do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], será preciso postar as alterações na lista de download para que os servidores de destino possam baixar novamente o trabalho atualizado. Para garantir que os servidores de destino possuam as definições de trabalho atuais, poste uma instrução INSERT após atualizar o trabalho multisservidor, da seguinte maneira:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Para notificar servidores de destino de que um trabalho multisservidor foi modificado, é necessário invocar o comando precedente, depois de usar um dos seguintes procedimentos:  
  
-   [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_update_jobstep (Transact-SQL)](https://msdn.microsoft.com/e158802c-c347-4a5d-bf75-c03e5ae56e6b)  
  
-   [sp_delete_jobstep (Transact-SQL)](https://msdn.microsoft.com/421ede8e-ad57-474a-9fb9-92f70a3e77e3)  
  
-   [Gerenciando eventos](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
-   [sp_detach_schedule (Transact-SQL)](https://msdn.microsoft.com/9a1fc335-1bef-4638-a33a-771c54a5dd19)  
  
    > [!NOTE]  
    > Não é necessário chamar **sp_post_msx_operation** depois de chamar **sp_update_job** ou **sp_delete_job**, pois esses procedimentos armazenados postam as alterações requeridas na lista de downloads automaticamente.  
  
As seguintes tarefas são comuns no gerenciamento de trabalhos em toda a empresa:  
  
**Para verificar o status de um servidor de destino**  
  
-   [Transact-SQL](https://msdn.microsoft.com/f841d3bd-901a-4980-ad0b-1c6eeba3f717)  
  
-   [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**Para alterar os servidores de destino quanto a um trabalho**  
  
-   [SQL Server Management Studio](../../ssms/agent/modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
-   [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**Para alterar o local de um servidor de destino**  
  
-   [SQL Server Management Studio](../../ssms/agent/specify-a-target-server-s-location-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
-   [SQL Server Management Objects (SMO)](https://msdn.microsoft.com/4cde2b85-2a31-4cac-8d16-7a4196066193)  
  
**Para sincronizar os relógios dos servidores de destino**  
  
-   [SQL Server Management Studio](../../ssms/agent/synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/40e44df7-d3e3-44ee-b149-08aba629a21f)  
  
**Para forçar um servidor de destino a sondar o servidor mestre**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar eventos](../../ssms/agent/manage-events.md)  
  
