---
title: Executar funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-udf
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6961d8306ff4b5a5f5280d25e3657952d0890063
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009517"
---
# <a name="execute-user-defined-functions"></a>Executar funções definidas pelo usuário
  Você pode executar uma função definida pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para executar uma definida pelo usuário funcione, usando:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 No Transact-SQL, os parâmetros podem ser fornecidos usando *valor* ou usando @*parameter_name*=*valor.* . Um parâmetro não faz parte de uma transação; portanto, se um parâmetro for alterado em uma transação que for posteriormente revertida, o parâmetro não será revertido para seu valor anterior. O valor retornado ao chamador será sempre o valor no momento do retorno do módulo.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Não são solicitadas permissões para executar a instrução EXECUTE. Porém, são solicitadas permissões nos protegíveis mencionados na cadeia de caracteres EXECUTE. Por exemplo, se a cadeia de caracteres tiver uma instrução INSERT, o chamador da instrução EXECUTE deverá ter a permissão INSERT na tabela de destino. As permissões são verificadas quando a instrução EXECUTE for encontrada, mesmo se ela estiver incluída em um módulo. Para obter mais informações, veja [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-execute-a-user-defined-function"></a>Para executar uma função definida pelo usuário  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Declares a variable and sets it to zero.  
    -- This variable is used to return the results of the function.  
    DECLARE @ret nvarchar(15)= NULL;   
  
    -- Executes the dbo.ufnGetSalesOrderStatusText function.  
    --The function requires a value for one parameter, @Status.   
    EXEC @ret = dbo.ufnGetSalesOrderStatusText @Status= 5;   
    --Returns the result in the message tab.  
    PRINT @ret;  
    ```  
  
 Para obter mais informações, veja [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
  
