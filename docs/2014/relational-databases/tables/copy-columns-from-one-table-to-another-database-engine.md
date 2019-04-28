---
title: Copiar colunas de uma tabela para outra (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67df7c541b0c664f200f6cf77affc0c809dbc719
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62736349"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>Copiar colunas de uma tabela em outra (Mecanismo de Banco de Dados)
  Este tópico descreve como copiar colunas de uma tabela para outra, copiando apenas a definição da coluna ou a definição e os dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para copiar colunas, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Quando uma coluna com um tipo de dados de alias é copiada de um banco de dados para outro, o tipo de dados de alias pode não estar disponível no banco de dados de destino. Nesse caso, a coluna receberá o tipo de dados base correspondente, mais próximo e disponível naquele banco de dados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
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
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse no nó **Exibições** e clique em **Nova Exibição**.  
  
3.  No menu **Designer de Consulta** , aponte para **Alterar Tipo**e clique em **Inserir Resultados**.  
  
4.  Na caixa de diálogo **Escolher Tabela de Destino para Inserir Resultados** , selecione a tabela em que serão copiados os dados e, em seguida, clique em **OK**.  
  
     Se você estiver copiando linhas em uma tabela, poderá adicionar a tabela de origem como tabela de destino.  
  
    > [!NOTE]  
    >  O**Designer de Consulta** não pode determinar antecipadamente quais tabelas e exibições poderão ser atualizadas. Portanto a lista de tabelas da caixa de diálogo **Escolher Tabela de Destino para Inserir Resultados** mostra todas as tabelas e exibições disponíveis na conexão de dados que está sendo consultada, até mesmo aquelas nas quais não é possível copiar linhas.  
  
5.  Clique com o botão direito do mouse no corpo do painel do diagrama e, no menu de atalho, clique em **Adicionar Tabela ao Diagrama**.  
  
6.  Na caixa de diálogo **Adicionar Tabela** , selecione as tabelas das quais você deseja copiar dados, clique em **Adicionar**e, em seguida, em **Fechar**.  
  
     As tabelas, em uma forma abreviada, aparecem no painel de diagrama.  
  
7.  Nas tabelas abreviadas, marque as caixas de todas as colunas das quais você deseja copiar dados.  
  
8.  No painel de critérios, na coluna **Anexar** , para cada coluna de destino escolha uma coluna da qual você deseja copiar dados.  
  
9. Especifique as linhas a serem copiadas inserindo critérios de pesquisa no painel de critérios. Para obter detalhes, veja [Especificar condições de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md).  
  
     Se você não especificar um critério de pesquisa, todas as linhas da tabela de origem serão copiadas na tabela de destino.  
  
10. Para copiar informações resumidas, especifique as opções **Agrupar por** . Para obter detalhes, veja [Resumir ou agregar valores para todas as linhas de uma tabela &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md).  
  
11. Clique no botão **Executar SQL** para executar a consulta.  
  
     Quando uma consulta para inserir resultados é executada, nenhum resultado é relatado no [Painel de Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). Em vez disso, será exibida uma mensagem indicando o total de linhas copiadas.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Para copiar definições de coluna de uma tabela para outra  
  
1.  Você não pode copiar colunas individuais de uma tabela para outra tabela existente usando instruções Transact-SQL. No entanto, pode criar uma tabela nova no grupo de arquivos padrão e insere nela as linhas resultantes da consulta usando SELECT INTO. Para obter mais informações, veja [INTO Clause &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-into-clause-transact-sql).  
  
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
  
  
