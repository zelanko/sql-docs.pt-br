---
title: Excluir chaves primárias | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing primary keys
- deleting primary keys
- primary keys [SQL Server], deleting
ms.assetid: c472e465-7bdd-4d74-8fc9-e47fca007ccb
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 2b80eb4c2f31ffe77fad7a12d07c9b729704c17f
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39544106"
---
# <a name="delete-primary-keys"></a>Excluir chaves primárias
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode excluir (descartar) uma chave primária no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Quando a chave primária é excluída, o índice correspondente é excluído.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para excluir uma chave primária usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-primary-key-constraint-using-object-explorer"></a>Para excluir uma restrição de chave primária usando o Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, expanda a tabela que contém a chave primária e expanda **Chaves**.  
  
2.  Clique com o botão direito do mouse na chave e selecione **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , verifique se a chave correta foi especificada e clique em **OK**.  
  
#### <a name="to-delete-a-primary-key-constraint-using-table-designer"></a>Para excluir uma restrição de chave primária usando o Designer de Tabela  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela com a chave primária e clique em **Design**.  
  
2.  Na grade de tabela, clique com o botão direito do mouse na linha com a chave primária e escolha **Remover Chave Primária** para alternar a configuração de ativado para desativado.  
  
    > [!NOTE]  
    >  Para desfazer essa ação, feche a tabela sem salvar as alterações. A exclusão de uma chave primária não pode ser desfeita sem perder todas as outras alterações feitas na tabela.  
  
3.  No menu **Arquivo**, clique em **Salvar***nome da tabela*.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-primary-key-constraint"></a>Para excluir uma restrição de chave primária  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo identifica primeiramente o nome da restrição de chave primária e depois exclui a restrição.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Return the name of primary key.  
    SELECT name  
    FROM sys.key_constraints  
    WHERE type = 'PK' AND OBJECT_NAME(parent_object_id) = N'TransactionHistoryArchive';  
    GO  
    -- Delete the primary key constraint.  
    ALTER TABLE Production.TransactionHistoryArchive  
    DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID;   
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) e [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)  
  
###  <a name="TsqlExample"></a>  
