---
description: Criar restrições exclusivas
title: Criar restrições exclusivas | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- UNIQUE_TSQL
helpviewer_keywords:
- UNIQUE constraints [SQL Server], creating
- constraints [SQL Server], creating
- constraints [SQL Server], unique
ms.assetid: a86f9d6f-f242-43be-b65d-b3435b71b62a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5a9be69bad3b4cad8265065d393bea75e107492f
ms.sourcegitcommit: fe5dedb2a43516450696b754e6fafac9f5fdf3cf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/31/2020
ms.locfileid: "89195092"
---
# <a name="create-unique-constraints"></a>Criar restrições exclusivas

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Você pode criar uma restrição exclusiva no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] para assegurar que nenhum valor duplicado seja digitado em colunas específicas que não integram uma chave primária. Criar uma restrição exclusiva cria automaticamente um índice exclusivo correspondente.  
  
> [!NOTE]    
> Confira [Chave primária, chave estrangeira e chave exclusiva no Azure Synapse Analytics](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-table-constraints) para obter informações sobre restrições exclusivas do Azure Synapse Analytics.
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar restrição exclusiva usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-unique-constraint"></a>Para criar restrição exclusiva  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela à qual você deseja adicionar uma restrição exclusiva e clique em **Design**.  
  
2.  No menu **Designer de Tabela** , clique em **Índices/Chaves**.  
  
3.  Na caixa de diálogo **Índices/Chaves** , clique em **Adicionar**.  
  
4.  Na grade, em **Geral**, clique em **Tipo** e selecione **Chave Exclusiva**, na caixa de listagem suspensa à direita da propriedade, e clique em **Fechar**.  
  
5.  No menu **Arquivo**, clique em **Salvar** _nome da tabela_.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-unique-constraint"></a>Para criar restrição exclusiva  
  
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
  
#### <a name="to-create-a-unique-constraint-on-an-existing-table"></a>Para criar uma restrição exclusiva em uma tabela existente  
  
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
  
#### <a name="to-create-a-unique-constraint-on-a-new-table"></a>Para criar uma restrição única em uma nova tabela  
  
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
  
     Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
