---
description: Exibir Atividade do Trabalho
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
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 04c42de9a98d507367cb2c2256a7c1f241baf1fc
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92030477"
---
# <a name="view-job-activity"></a>Exibir Atividade do Trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Este tópico descreve como exibir o estado de runtime de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Quando o serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado, é criada uma sessão e a tabela **sysjobactivity** no banco de dados **msdb** é preenchida com todas as tarefas definidas existentes. Essa tabela registra atividade e status do trabalho atual. Você pode usar o Monitor de Atividade do Trabalho no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para exibir o estado atual dos trabalhos. Se o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for concluído inesperadamente, pode-se recorrer à tabela **sysjobactivity** para consultar quais trabalhos estavam sendo executados quando o serviço foi finalizado.  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="security"></a><a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-view-job-activity"></a>Para exibir atividade do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e expanda-a.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Monitor de Atividade do Trabalho** e clique em **Exibir Atividade do Trabalho**.  
  
4.  Em **Monitor de Atividade do Trabalho**, é possível exibir detalhes sobre cada trabalho que está definido para esse servidor.  
  
5.  Clique com o botão direito do mouse em um trabalho para que ele seja iniciado, interrompido, habilitado ou desabilitado; tenha seu status atualizado conforme exibido no Monitor de Atividade do Trabalho; seja excluído, ou para que seu histórico ou propriedades sejam exibidos.  Para iniciar, interromper, habilitar ou desabilitar ou atualizar vários trabalhos, selecione várias linhas, no Monitor de Atividade do Trabalho, e clique com o botão direito do mouse para fazer sua seleção.  
  
6.  Para atualizar o Monitor de Atividade do Trabalho, clique em **Atualizar**. Para exibir menos linhas, clique em **Filtrar** e digite parâmetros de filtro.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Usando Transact-SQL  
  
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
  
Para obter mais informações, consulte [sp_help_jobactivity (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql.md).  
