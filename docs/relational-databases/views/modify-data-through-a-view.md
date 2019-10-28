---
title: Modificar dados por meio de uma exibição | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e41abc4ab3f798a3ee970061ddc21539403ef6b
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907504"
---
# <a name="modify-data-through-a-view"></a>Modificar dados por meio de uma exibição
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  Você pode modificar os dados de uma tabela base subjacente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Consulte a seção “Exibições atualizáveis” em [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
  
###  <a name="Permissions"></a> Permissões  
 Exige a permissão UPDATE, INSERT ou DELETE na tabela de destino, dependendo da ação em execução.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>Para modificar os dados da tabela por uma exibição  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição e expanda **Exibições**.  
  
2.  Clique com o botão direito do mouse na exibição e selecione **Editar 200 Linhas Superiores**.  
  
3.  Você pode precisar modificar a instrução SELECT no painel **SQL** para retornar as linhas a serem modificadas.  
  
4.  No painel **Resultados** , localize a linha a ser alterada ou excluída. Para excluir a linha, clique com o botão direito do mouse na linha e selecione **Excluir**. Para alterar dados em uma ou mais colunas, modifique os dados na coluna.  
  
    > **IMPORTANTE:** Você não poderá excluir uma linha se a exibição referenciar mais de uma tabela base. Você pode atualizar somente colunas que pertencem a uma única tabela base.  
  
5.  Para inserir uma linha, role até o fim das linhas e insira os novos valores.  

    > **IMPORTANTE:** Você não poderá inserir uma linha se a exibição referenciar mais de uma tabela base.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>Para atualizar os dados da tabela por uma exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
 Para obter mais informações, consulte [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md).  
  
#### <a name="to-insert-table-data-through-a-view"></a>Para inserir os dados da tabela por uma exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo insere uma nova linha na tabela base `HumanResouces.Department` especificando as colunas pertinentes da exibição `HumanResources.vEmployeeDepartmentHistory`. A instrução tem sucesso porque somente as colunas de uma tabela base são especificadas e as outras colunas na tabela base têm valores padrão.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 Para obter mais informações, consulte [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
  
