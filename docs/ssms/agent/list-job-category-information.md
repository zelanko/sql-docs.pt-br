---
title: "Listar informações de categoria do trabalho | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6707983f3fe707a5253ff6722adb190579bd1d48
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="list-job-category-information"></a>Listar informações de categoria de trabalho
Este tópico descreve como listas informações de categoria de trabalho no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[tsql](../../includes/tsql_md.md)] ou o SQL Server Management Objects.  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para listar informações de categoria de trabalho usando**  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server Management Objects](#SMO)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>Para listar informações de categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_help_category (Transact-SQL)](http://msdn.microsoft.com/en-us/8cad1dcc-b43e-43bd-bea0-cb0055c84169).  
  
## <a name="SMO"></a>Usando o SQL Server Management Objects  
**Para listar informações de categoria de trabalho**  
  
Use a classe **JobCategory** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell.  
  

