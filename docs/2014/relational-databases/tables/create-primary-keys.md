---
title: Criar chaves primárias | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
author: stevestein
ms.author: sstein
ms.openlocfilehash: c515ef8f978b41225ff45e87646b0aa7a9706a34
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85014861"
---
# <a name="create-primary-keys"></a>Criar chaves primárias
  Você pode definir uma chave primária no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Criar uma chave primária cria automaticamente um índice correspondente exclusivo, clusterizado ou não clusterizado.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma chave primária usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Uma tabela pode conter apenas uma restrição PRIMARY KEY.  
  
-   Todas as colunas definidas em uma restrição PRIMARY KEY devem ser definidas como NOT NULL. Se a nulidade não for especificada, todas as colunas participantes de uma restrição FOREIGN KEY devem ter sua nulidade definida como NOT NULL.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 A criação de uma nova tabela com uma chave primária requer a permissão CREATE TABLE no banco de dados e a permissão ALTER no esquema no qual a tabela está sendo criada.  
  
 Criar uma chave primária em uma tabela existente requer a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-primary-key"></a>Para criar uma chave primária  
  
1.  No Pesquisador de objetos, clique com o botão direito do mouse na tabela à qual você deseja adicionar uma restrição exclusiva e clique em **design**.  
  
2.  No **Designer de Tabela**, clique no seletor de linha para a coluna de banco de dados que você deseja definir como chave primária. Se desejar selecionar colunas múltiplas, digite a tecla CTRL enquanto você clica nos seletores de linha para as outras colunas.  
  
3.  Clique com o botão direito do mouse no seletor de linha da coluna e selecione **Definir Chave Primária**.  
  
> [!CAUTION]  
>  Se você quiser redefinir a chave primária, qualquer relação com a chave primária existente deve ser excluída antes que a nova chave primária seja criada. Uma mensagem avisará que as relações existentes serão excluídas automaticamente como parte desse processo.  
  
 Uma coluna de chave primária é identificada por um símbolo de chave primária em seu seletor de linha.  
  
 Se uma chave primária consistir em mais de uma coluna, serão permitidos valores duplicados em uma coluna, mas cada combinação de valores de todas as colunas na chave primária deve ser única.  
  
 Se você definir uma chave combinada, a ordem das colunas na chave primária corresponderá à ordem das colunas, como é mostrado na tabela. Entretanto, você poderá alterar a ordem de colunas depois que a chave primária for criada. Para obter mais informações, veja [Modificar chaves primárias](modify-primary-keys.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-primary-key-in-an-existing-table"></a>Para criar uma chave primária em uma tabela existente  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma chave primária no coluna `TransactionID`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Production.TransactionHistoryArchive   
    ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);  
    GO  
  
    ```  
  
#### <a name="to-create-a-primary-key-in-a-new-table"></a>Para criar uma chave primária em uma nova tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma tabela e define uma chave primária na coluna `TransactionID`.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive1  
    (  
       TransactionID int NOT NULL,  
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
    );  
    GO  
  
    ```  
  
     Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql), [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) e [table_constraint &#40;Transact-SQL&#41;](/sql/relational-databases/system-information-schema-views/table-constraints-transact-sql).  
  
###  <a name="TsqlExample"></a>  
