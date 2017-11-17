---
title: Renomear tabelas (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
ms.assetid: 2f5c922d-4d71-4694-9fca-28dd99375799
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d65c475509d57577f691e656157c7754c7d8549f
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="rename-tables-database-engine"></a>Renomear tabelas (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode renomear uma tabela no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!CAUTION]  
>  Pense cuidadosamente antes de renomear uma tabela. Se as consultas, as exibições, as funções definidas pelo usuário, os procedimentos armazenados ou os programas existentes se referirem à tabela, a modificação do nome tornará esses objetivos inválidos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Renomear uma tabela não renomeia automaticamente as referências a essa tabela. É necessário modificar manualmente todos os objetos que fazem referência à tabela renomeada. Por exemplo, se você renomear uma tabela e essa tabela for referenciada em um gatilho, será necessário modificar o gatilho para que ele reflita o novo nome da tabela. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para listar as dependências dessa tabela antes de renomeá-la.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-a-table"></a>Para renomear uma tabela  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela que você deseja renomear e escolha **Design** no menu de atalho.  
  
2.  No menu **Exibir** , escolha **Propriedades**.  
  
3.  No campo do valor **Nome** , na janela **Propriedades** , digite um novo nome para a tabela.  
  
4.  Para cancelar essa ação, pressione a tecla ESC antes de deixar o campo.  
  
5.  No menu **Arquivo** , escolha **Salvar***table name*.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-rename-a-table"></a>Para renomear uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  O exemplo a seguir renomeia a tabela `SalesTerritory` como `SalesTerr` no esquema `Sales` . Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
    ```  
  
 Para obter exemplos adicionais, consulte [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  

