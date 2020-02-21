---
title: Exibir Atividade do Trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 817e09e25695f985de8397bca5436da817deda2d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254746"
---
# <a name="view-job-activity"></a>Exibir Atividade do Trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como exibir o estado de runtime de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Quando o serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado, é criada uma sessão e a tabela **sysjobactivity** no banco de dados **msdb** é preenchida com todas as tarefas definidas existentes. Essa tabela registra atividade e status do trabalho atual. Você pode usar o Monitor de Atividade do Trabalho no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para exibir o estado atual dos trabalhos. Se o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for concluído inesperadamente, pode-se recorrer à tabela **sysjobactivity** para consultar quais trabalhos estavam sendo executados quando o serviço foi finalizado.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-view-job-activity"></a>Para exibir atividade do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e expanda-a.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Monitor de Atividade do Trabalho** e clique em **Exibir Atividade do Trabalho**.  
  
4.  Em **Monitor de Atividade do Trabalho**, é possível exibir detalhes sobre cada trabalho que está definido para esse servidor.  
  
5.  Clique com o botão direito do mouse em um trabalho para que ele seja iniciado, interrompido, habilitado ou desabilitado; tenha seu status atualizado conforme exibido no Monitor de Atividade do Trabalho; seja excluído, ou para que seu histórico ou propriedades sejam exibidos.  Para iniciar, interromper, habilitar ou desabilitar ou atualizar vários trabalhos, selecione várias linhas, no Monitor de Atividade do Trabalho, e clique com o botão direito do mouse para fazer sua seleção.  
  
6.  Para atualizar o Monitor de Atividade do Trabalho, clique em **Atualizar**. Para exibir menos linhas, clique em **Filtrar** e digite parâmetros de filtro.  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-view-job-activity"></a>Para exibir atividade do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- lists activity for all jobs that the current user has permission to view.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobactivity ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_help_jobactivity (Transact-SQL)](https://msdn.microsoft.com/d344864f-b4d3-46b1-8933-b81dec71f511).  
  
