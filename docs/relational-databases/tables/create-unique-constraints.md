---
title: "Criar restri&#231;&#245;es exclusivas | Microsoft Docs"
ms.custom: ""
ms.date: "10/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "UNIQUE_TSQL"
helpviewer_keywords: 
  - "restrições UNIQUE [SQL Server], criando"
  - "restrições [SQL Server], criando"
  - "restrições [SQL Server], unique"
ms.assetid: a86f9d6f-f242-43be-b65d-b3435b71b62a
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Criar restri&#231;&#245;es exclusivas
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode criar uma restrição exclusiva no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] para assegurar que nenhum valor duplicado seja digitado em colunas específicas que não integram uma chave primária. Criar uma restrição exclusiva cria automaticamente um índice exclusivo correspondente.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar restrição exclusiva usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para criar restrição exclusiva  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela à qual você deseja adicionar uma restrição exclusiva e clique em **Design**.  
  
2.  No menu **Designer de Tabela**, clique em **Índices/Chaves**.  
  
3.  Na caixa de diálogo **Índices/Chaves**, clique em **Adicionar**.  
  
4.  Na grade, em **Geral**, clique em **Tipo** e selecione **Chave Exclusiva** na caixa de listagem suspensa à direita da propriedade.  
  
5.  No menu **Arquivo** , clique em **Salvar***table name*.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para criar restrição exclusiva  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria a tabela `TransactionHistoryArchive4` e cria uma restrição exclusiva na coluna `TransactionID`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive4  
     (  
       TransactionID int NOT NULL,   
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)   
    );   
    GO  
  
    ```  
  
#### Para criar uma restrição exclusiva em uma tabela existente  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma restrição exclusiva nas colunas `PasswordHash` e `PasswordSalt` na tabela `Person.Password`.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    ALTER TABLE Person.Password   
    ADD CONSTRAINT AK_Password UNIQUE (PasswordHash, PasswordSalt);   
    GO  
  
    ```  
  
#### Para criar uma restrição exclusiva em uma nova tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma tabela e define uma restrição exclusiva na coluna `TransactionID`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive2  
    (  
       TransactionID int NOT NULL,  
       CONSTRAINT AK_TransactionID UNIQUE(TransactionID)  
    );  
    GO  
  
    ```  
  
     Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [table_constraint &#40;Transact-SQL&#41;](../Topic/table_constraint%20\(Transact-SQL\).md).  
  
###  <a name="TsqlExample"></a>  