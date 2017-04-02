---
title: "Excluir restri&#231;&#245;es exclusivas | Microsoft Docs"
ms.custom: ""
ms.date: "10/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "removendo restrições"
  - "restrições UNIQUE [SQL Server], excluindo"
  - "restrições [SQL Server], excluindo"
  - "excluindo restrições"
  - "restrições [SQL Server], unique"
ms.assetid: 71e563fc-f5d7-4c2e-a42f-f0695a831f32
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Excluir restri&#231;&#245;es exclusivas
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode excluir uma restrição exclusiva no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Excluir uma restrição exclusiva remove o requisito de exclusividade dos valores inseridos na coluna ou da combinação de colunas incluídas na expressão de restrição e exclui o índice exclusivo correspondente.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para excluir uma restrição exclusiva usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para excluir uma restrição exclusiva usando o Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, expanda a tabela que contém a restrição exclusiva e expanda **Restrições**.  
  
2.  Clique com o botão direito do mouse na chave e selecione **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , verifique se a chave correta foi especificada e clique em **OK**.  
  
#### Para excluir uma restrição exclusiva usando o Designer de Tabela  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela com a restrição exclusiva e clique em **Design**.  
  
2.  No menu **Designer de Tabela**, clique em **Índices/Chaves**.  
  
3.  Na caixa de diálogo **Índices/Chaves**, selecione a chave exclusiva na lista **Índice e Chave Primária / Exclusiva Selecionada**.  
  
4.  Clique em **Excluir**.  
  
5.  No menu **Arquivo** , clique em **Salvar** *table name*.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para excluir uma restrição exclusiva  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Return the name of unique constraint.  
    SELECT name  
    FROM sys.objects  
    WHERE type = 'UQ' AND OBJECT_NAME(parent_object_id) = N' DocExc';  
    GO  
    -- Delete the unique constraint.  
    ALTER TABLE dbo.DocExc   
    DROP CONSTRAINT UNQ_ColumnB_DocExc;  
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) e [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  