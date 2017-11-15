---
title: Exibir atividade do trabalho | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e27c4e63d9484de2de699c9e79549ac7809ee76
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="view-job-activity"></a>Exibir Atividade do Trabalho
Este tópico descreve como exibir o estado de tempo de execução de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
Quando o serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é iniciado, uma sessão nova é criada e a tabela **sysjobactivity** no banco de dados **msdb** é preenchida com todas as tarefas definidas existentes. Essa tabela registra atividade e status do trabalho atual. Você pode usar o Monitor de Atividade do Trabalho no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para exibir o estado atual dos trabalhos. Se o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent for concluído inesperadamente, pode-se recorrer à tabela **sysjobactivity** para consultar quais trabalhos estavam sendo executados quando o serviço foi finalizado.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para exibir a atividade do trabalho usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
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
  
Para obter mais informações, consulte [sp_help_jobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/d344864f-b4d3-46b1-8933-b81dec71f511).  
  
