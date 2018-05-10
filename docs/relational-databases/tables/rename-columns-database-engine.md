---
title: Renomear colunas (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], names
- renaming columns
- column names [SQL Server]
ms.assetid: 7c71ec9f-0180-4398-b32a-4bfb7592e75d
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6f49a47ebfe4e529c11fc0d1b79d7eec5896f13f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rename-columns-database-engine"></a>Renomear colunas (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Você pode renomear uma coluna de tabela no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear colunas, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Renomear uma coluna não renomeia automaticamente as referências a essa coluna. É necessário modificar manualmente todos os objetos que fazem referência à coluna renomeada. Por exemplo, se você renomear uma coluna de tabela e aquela coluna for referenciada em um gatilho, será necessário modificar o gatilho para que ele reflita o nome novo da coluna. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para listar as dependências do objeto antes de renomeá-lo.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no objeto.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-a-column-using-object-explorer"></a>Para renomear uma coluna usando o Pesquisador de Objetos  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela na qual você deseja renomear colunas e selecione **Renomear**.  
  
3.  Digite um novo nome para a coluna.  
  
#### <a name="to-rename-a-column-using-table-designer"></a>Para renomear uma coluna usando o Designer de Tabela  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela na qual você deseja renomear colunas e selecione **Design**.  
  
2.  Em **Nome da Coluna**, selecione o nome que você deseja alterar e digite um nome novo.  
  
3.  No menu **Arquivo**, clique em **Salvar***nome da tabela*.  
  
> [!NOTE]  
>  Você também pode alterar o nome de uma coluna na guia **Propriedades da Coluna** . Selecione a coluna cujo nome você deseja alterar e digite um novo valor para **Nome**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para renomear uma coluna**  
  
#### <a name="to-rename-a-column"></a>Para renomear uma coluna  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  O exemplo a seguir renomeia a coluna `TerritoryID` na tabela `Sales.SalesTerritory` como `TerrID`. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
    GO  
    ```  
  
 Para obter mais informações, veja [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  
