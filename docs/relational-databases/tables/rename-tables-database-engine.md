---
description: Renomear tabelas (Mecanismo de Banco de Dados)
title: Renomear tabelas (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a26a851196e5357e04f3f31b405a3fb6738a49de
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440517"
---
# <a name="rename-tables-database-engine"></a>Renomear tabelas (Mecanismo de Banco de Dados)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Renomear uma tabela no Banco de Dados do SQL Server ou SQL do Azure.

Para renomear uma tabela no Azure Synapse Analytics ou no Parallel Data Warehouse, use a instrução t-sql [RENAME OBJECT](../../t-sql/statements/rename-transact-sql.md). 
  
> [!CAUTION]  
>  Pense cuidadosamente antes de renomear uma tabela. Se as consultas, as exibições, as funções definidas pelo usuário, os procedimentos armazenados ou os programas existentes se referirem à tabela, a modificação do nome tornará esses objetivos inválidos.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 Renomear uma tabela não renomeia automaticamente as referências a essa tabela. É necessário modificar manualmente todos os objetos que fazem referência à tabela renomeada. Por exemplo, se você renomear uma tabela e essa tabela for referenciada em um gatilho, será necessário modificar o gatilho para que ele reflita o novo nome da tabela. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para listar as dependências dessa tabela antes de renomeá-la.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-a-table"></a>Para renomear uma tabela  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela que você deseja renomear e escolha **Design** no menu de atalho.  
  
2.  No menu **Exibir** , escolha **Propriedades**.  
  
3.  No campo do valor **Nome** , na janela **Propriedades** , digite um novo nome para a tabela.  
  
4.  Para cancelar essa ação, pressione a tecla ESC antes de deixar o campo.  
  
5.  No menu **Arquivo**, escolha ***Salvar** _nome da tabela_.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
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
  
  
