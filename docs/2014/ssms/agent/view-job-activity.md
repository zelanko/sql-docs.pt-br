---
title: Exibir atividade do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fc6099fa9f523b351489ce4301596aeb90c1509
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782568"
---
# <a name="view-job-activity"></a>Exibir Atividade do Trabalho
  Este tópico descreve como exibir o estado de tempo de execução de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Quando o serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado, uma sessão nova é criada e a tabela **sysjobactivity** no banco de dados **msdb** é preenchida com todas as tarefas definidas existentes. Essa tabela registra atividade e status do trabalho atual. Você pode usar o Monitor de Atividade do Trabalho no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para exibir o estado atual dos trabalhos. Se o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent for concluído inesperadamente, pode-se recorrer à tabela **sysjobactivity** para consultar quais trabalhos estavam sendo executados quando o serviço foi finalizado.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir a atividade do trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-job-activity"></a>Para exibir atividade do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Monitor de Atividade do Trabalho** e clique em **Exibir Atividade do Trabalho**.  
  
4.  Em **Monitor de Atividade do Trabalho**, é possível exibir detalhes sobre cada trabalho que está definido para esse servidor.  
  
5.  Clique com o botão direito do mouse em um trabalho para que ele seja iniciado, interrompido, habilitado ou desabilitado; tenha seu status atualizado conforme exibido no Monitor de Atividade do Trabalho; seja excluído, ou para que seu histórico ou propriedades sejam exibidos.  Para iniciar, interromper, habilitar ou desabilitar ou atualizar vários trabalhos, selecione várias linhas, no Monitor de Atividade do Trabalho, e clique com o botão direito do mouse para fazer sua seleção.  
  
6.  Para atualizar o Monitor de Atividade do Trabalho, clique em **Atualizar**. Para exibir menos linhas, clique em **Filtrar** e digite parâmetros de filtro.  
  
##  <a name="TSQL"></a> Usando Transact-SQL  
  
#### <a name="to-view-job-activity"></a>Para exibir atividade do trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- lists activity for all jobs that the current user has permission to view.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobactivity ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_help_jobactivity &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql).  
  
  
