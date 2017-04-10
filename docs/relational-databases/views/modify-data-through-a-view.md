---
title: "Modificar dados por meio de uma exibi&#231;&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "10/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-views"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modificações de dados [SQL Server], exibições"
  - "exibições [SQL Server], modificando dados por meio de"
  - "modificando dados [SQL Server], exibições"
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Modificar dados por meio de uma exibi&#231;&#227;o
  Você pode modificar os dados de uma tabela base subjacente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Consulte a seção “Exibições atualizáveis” em [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
  
###  <a name="Permissions"></a> Permissões  
 Exige a permissão UPDATE, INSERT ou DELETE na tabela de destino, dependendo da ação em execução.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para modificar os dados da tabela por uma exibição  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição e expanda **Exibições**.  
  
2.  Clique com o botão direito do mouse na exibição e selecione **Editar 200 Linhas Superiores**.  
  
3.  Você pode precisar modificar a instrução SELECT no painel **SQL** para retornar as linhas a serem modificadas.  
  
4.  No painel **Resultados** , localize a linha a ser alterada ou excluída. Para excluir a linha, clique com o botão direito do mouse na linha e selecione **Excluir**. Para alterar dados em uma ou mais colunas, modifique os dados na coluna.  
  
    > **IMPORTANTE:** Você não poderá excluir uma linha se a exibição referenciar mais de uma tabela base. Você pode atualizar somente colunas que pertencem a uma única tabela base.  
  
5.  Para inserir uma linha, role até o fim das linhas e insira os novos valores.  
  
    > **IMPORTANTE:** Você não poderá inserir uma linha se a exibição referenciar mais de uma tabela base.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para atualizar os dados da tabela por uma exibição  
  
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
  
#### Para inserir os dados da tabela por uma exibição  
  
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
  
  