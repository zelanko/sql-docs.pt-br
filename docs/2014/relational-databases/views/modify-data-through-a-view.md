---
title: Modificar dados por meio de uma exibição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-views
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fbc9d4bd90bea3dd6589fd92c8548653c5315d02
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119298"
---
# <a name="modify-data-through-a-view"></a>Modificar dados por meio de uma exibição
  Você pode modificar os dados de uma tabela base subjacente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para modificar os dados de tabela por meio de uma exibição, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Consulte a seção “Exibições atualizáveis” em [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão UPDATE, INSERT ou DELETE na tabela de destino, dependendo da ação em execução.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>Para modificar os dados da tabela por uma exibição  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição e expanda **Exibições**.  
  
2.  Clique com o botão direito do mouse na exibição e selecione **Editar 200 Linhas Superiores**.  
  
3.  Você pode precisar modificar a instrução SELECT no painel **SQL** para retornar as linhas a serem modificadas.  
  
4.  No painel **Resultados** , localize a linha a ser alterada ou excluída. Para excluir a linha, clique com o botão direito do mouse na linha e selecione **Excluir**. Para alterar dados em uma ou mais colunas, modifique os dados na coluna.  
  
    > [!IMPORTANT]  
    >  Você não poderá excluir uma linha se a exibição referenciar mais de uma tabela base. Você pode atualizar somente colunas que pertencem a uma única tabela base.  
  
5.  Para inserir uma linha, role até o fim das linhas e insira os novos valores.  
  
    > [!IMPORTANT]  
    >  Você não poderá inserir uma linha se a exibição referenciar mais de uma tabela base.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>Para atualizar os dados da tabela por uma exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo altera o valor nas colunas `StartDate` e `EndDate` para um funcionário específico referenciando colunas na exibição `HumanResources.vEmployeeDepartmentHistory`. Esta exibição retorna valores de duas tabelas. Esta instrução tem sucesso porque as colunas modificadas são apenas de uma das tabelas base.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    UPDATE HumanResources.vEmployeeDepartmentHistory  
    SET StartDate = '20110203', EndDate = GETDATE()   
    WHERE LastName = N'Smith' AND FirstName = 'Samantha';   
    GO  
    ```  
  
 Para obter mais informações, consulte [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql).  
  
#### <a name="to-insert-table-data-through-a-view"></a>Para inserir os dados da tabela por uma exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo insere uma nova linha na tabela base `HumanResouces.Department` especificando as colunas pertinentes da exibição `HumanResources.vEmployeeDepartmentHistory`. A instrução tem sucesso porque somente as colunas de uma tabela base são especificadas e as outras colunas na tabela base têm valores padrão.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 Para obter mais informações, consulte [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql).  
  
  
