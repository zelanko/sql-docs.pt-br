---
title: Copiar colunas de uma tabela para outra (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b3195e1f826dde57dba9113efa51733b2a3bd1dd
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395813"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>Copiar colunas de uma tabela em outra (Mecanismo de Banco de Dados)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

  Este tópico descreve como copiar colunas de uma tabela para outra, copiando apenas a definição da coluna ou a definição e os dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para copiar colunas, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 Quando uma coluna com um tipo de dados de alias é copiada de um banco de dados para outro, o tipo de dados de alias pode não estar disponível no banco de dados de destino. Nesse caso, a coluna receberá o tipo de dados base correspondente, mais próximo e disponível naquele banco de dados.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Para copiar definições de coluna de uma tabela para outra  
  
1.  Abra a tabela que contém as colunas a serem copiadas e a tabela na qual deseja copiar as colunas clicando com o botão direito do mouse nas tabelas e clicando em **Design**.  
  
2.  Clique na guia da tabela que contém as colunas a serem copiadas e selecione as colunas.  
  
3.  No menu **Editar** clique em **Copiar**.  
  
4.  Clique na guia da tabela, na qual você pretende copiar as colunas.  
  
5.  Selecione a coluna à qual se seguirão as colunas inseridas e, no menu **Editar** , clique em **Colar**.  

#### <a name="to-copy-data-from-one-table-to-another"></a>Para copiar dados de uma tabela para outra  
  
1.  Siga as orientações para copiar as definições da coluna acima.  
  
    > [!NOTE]  
    >  Antes de começar a copiar dados de uma tabela para outra, verifique se os tipos de dados nas colunas de destino são compatíveis com os tipos de dados das colunas de origem.  
  
2.  Abre uma nova janela do Editor de Consultas. 

3.  Clique com o botão direito do mouse no Editor de Consultas e clique em **Projetar Consulta no Editor**. 

4.  Na caixa de diálogo **Adicionar Tabela** , selecione a tabela de origem e de destino, clique em **Adicionar**e feche a caixa de diálogo **Adicionar Tabela** . 

5.  Clique com o botão direito do mouse em uma área aberta do Editor de Consultas, aponte para **Alterar Tipo**, e clique em **Inserir Resultados**.  

6.  Na caixa de diálogo **Escolher Tabela de Destino para Inserir Resultados** , selecione a tabela de destino. 

7.  Na parte superior do Designer de Consultas, clique na coluna de origem da tabela de origem.

8. O Designer de Consultas agora criou uma consulta INSERT. Clique em OK para colocar a consulta na janela original do Editor de Consultas.  

9.  Execute a consulta para inserir os dados da tabela de origem na tabela de destino.

  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Para copiar definições de coluna de uma tabela para outra  
  
1.  Você não pode copiar colunas individuais de uma tabela para outra tabela existente usando instruções Transact-SQL. No entanto, pode criar uma tabela nova no grupo de arquivos padrão e insere nela as linhas resultantes da consulta usando SELECT INTO. Para obter mais informações, veja [INTO Clause &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md).  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>Para copiar dados de uma tabela para outra  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
