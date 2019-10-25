---
title: Listar informações de categoria do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dae8f1d98fb1758e9a9802883def1574bda68a78
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798209"
---
# <a name="list-job-category-information"></a>Listar informações de categoria de trabalho
  Como listar informações de categoria de trabalho em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)] ou SQL Server Management Objects.  

  
##  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  

  
##  <a name="TSQL"></a> Usando Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>Para listar informações de categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 Para obter mais informações, [consulte &#40;Transact-SQL&#41;sp_help_category](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql).  
  
  
##  <a name="SMO"></a>Usando SQL Server Management Objects  
 **Para listar informações de categoria de trabalho**  
  
 Use a classe `JobCategory` usando uma linguagem de programação que você possa escolher, como Visual Basic, Visual C# ou PowerShell. Para obter mais informações, [consulte &#40;SQL Server Management Objects&#41; o guia de programação do Smo](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md).  
