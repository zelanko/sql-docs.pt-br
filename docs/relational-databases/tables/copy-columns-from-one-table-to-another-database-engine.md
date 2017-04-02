---
title: "Copiar colunas de uma tabela em outra (Mecanismo de Banco de Dados) | Microsoft Docs"
ms.custom: ""
ms.date: "09/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "copiando colunas"
  - "colunas [SQL Server], copiando"
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Copiar colunas de uma tabela em outra (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

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
  
#### Para copiar definições de coluna de uma tabela para outra  
  
1.  Abra a tabela que contém as colunas a serem copiadas e a tabela na qual deseja copiar as colunas clicando com o botão direito do mouse nas tabelas e clicando em **Design**.  
  
2.  Clique na guia da tabela que contém as colunas a serem copiadas e selecione as colunas.  
  
3.  No menu **Editar** clique em **Copiar**.  
  
4.  Clique na guia da tabela, na qual você pretende copiar as colunas.  
  
5.  Selecione a coluna à qual se seguirão as colunas inseridas e, no menu **Editar** , clique em **Colar**.  
  
#### Para copiar dados de uma tabela para outra  
  
1.  Siga as orientações para copiar as definições da coluna acima.  
  
    > [!NOTE]  
    >  Antes de começar a copiar dados de uma tabela para outra, verifique se os tipos de dados nas colunas de destino são compatíveis com os tipos de dados das colunas de origem.  
  
2.  Abre uma nova janela do Editor de Consultas. 

3.  Clique com o botão direito do mouse no Editor de Consultas e clique em **Projetar Consulta no Editor.**. 

4.  Na caixa de diálogo **Adicionar Tabela**, selecione a tabela de origem e de destino, clique em **Adicionar** e feche a caixa de diálogo **Adicionar Tabela**. 

5.  Clique com o botão direito do mouse em uma área aberta do Editor de Consultas, aponte para **Alterar Tipo**, e clique em **Inserir Resultados**.  

6.  Na caixa de diálogo **Escolher Tabela de Destino para Inserir Resultados**, selecione a tabela de destino. 

7.  Na parte superior do Designer de Consultas, clique na coluna de origem da tabela de origem.

8. O Designer de Consultas agora criou uma consulta INSERT. Clique em OK para colocar a consulta na janela original do Editor de Consultas.  

9.  Execute a consulta para inserir os dados da tabela de origem na tabela de destino.

  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para copiar definições de coluna de uma tabela para outra  
  
1.  Você não pode copiar colunas individuais de uma tabela para outra tabela existente usando instruções Transact-SQL. No entanto, pode criar uma tabela nova no grupo de arquivos padrão e insere nela as linhas resultantes da consulta usando SELECT INTO. Para obter mais informações, veja [INTO Clause &#40;Transact-SQL&#41;](../Topic/INTO%20Clause%20\(Transact-SQL\).md).  
  
#### Para copiar dados de uma tabela para outra  
  
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
  
  