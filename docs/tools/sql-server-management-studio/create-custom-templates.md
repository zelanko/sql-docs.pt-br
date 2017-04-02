---
title: "Criar modelos personalizados | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "tql"
  - "modelos [Transact-SQL], criando"
  - "modelos [Transact-SQL]"
ms.assetid: 41098e78-b482-410e-bfe8-2ac10769ac4a
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Criar modelos personalizados
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é fornecido com modelos para várias tarefas comuns, mas o poder real dos modelos está na capacidade de criar um modelo personalizado para um script complexo que deve ser criado com frequência. Nesta prática, você criará um script simples com poucos parâmetros, mas modelos também são úteis para scripts longos e repetitivos.  
  
## Usando modelos personalizados  
  
#### Para criar um modelo personalizado  
  
1.  No Gerenciador de Modelos, expanda **Modelos do SQL Server**, clique com o botão direito do mouse em **Procedimento Armazenado**, aponte para **Novo** e clique em **Pasta**.  
  
2.  Digite **Personalizado** como o nome da nova pasta de modelos e pressione ENTER.  
  
3.  Clique com o botão direito do mouse em **Personalizado**, aponte para **Novo** e clique em **Modelo**.  
  
4.  Digite **WorkOrdersProc** como o nome do novo modelo e pressione **Enter**.  
  
5.  Clique com o botão direito do mouse em **WorkOrdersProc** e clique em **Editar**.  
  
6.  Na caixa de diálogo **Conectar ao Mecanismo de Banco de Dados**, verifique as informações da conexão e clique em **Conectar**.  
  
7.  No Editor de Consultas, digite o script a seguir para criar um procedimento armazenado que procura pedidos de uma peça específica, neste caso, a Lâmina. (Você pode copiar e colar o código da janela Tutorial.)  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersForBlade')  
       DROP PROCEDURE dbo.WorkOrdersForBlade;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersForBlade  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = 'Blade';  
    GO  
    ```  
  
8.  Pressione F5 para executar esse script, criando o procedimento **WorkOrdersForBlade**.  
  
9. No Pesquisador de Objetos, clique com o botão direito do mouse no servidor e clique em **Nova Consulta**. Uma nova janela do Editor de Consultas é aberta.  
  
10. No Editor de Consultas, digite **EXECUTE dbo.WorkOrdersForBlade** e pressione F5 para executar a consulta. Confirme se o painel **Resultados** retorna uma lista dos pedidos de trabalho nas folhas.  
  
11. Edite o script de modelo (o script da etapa 7), substituindo o nome de produto Folha pelo parâmetro ***\<*product_name**, **nvarchar(50)**, **name*>***, em quatro lugares.  
  
    > [!NOTE]  
    > Parâmetros requerem três elementos: o nome do parâmetro que você deseja substituir, o tipo de dados do parâmetro e um valor padrão do parâmetro.  
  
12. Agora o script deve ter a seguinte aparência:  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersFor<product_name, nvarchar(50), name>')  
       DROP PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = '<product_name, nvarchar(50), name>';  
    GO  
    ```  
  
13. No menu **Arquivo**, clique em **Salvar WorkOrdersProc.sql** para salvar o modelo.  
  
#### Para testar o modelo personalizado  
  
1.  No Gerenciador de Modelos, expanda **Procedimento Armazenado**, expanda **Personalizado** e clique duas vezes em **WorkOrderProc**.  
  
2.  Na caixa de diálogo **Conectar ao Mecanismo de Banco de Dados**, complete as informações de conexão e clique em **Conectar**. Uma nova janela do Editor de Consultas será aberta, exibindo o conteúdo do modelo **WorkOrderProc**.  
  
3.  No menu **Consulta** , clique em **Especificar Valores para Parâmetros de Modelo**.  
  
4.  Na caixa de diálogo **Substituir Parâmetros do Modelo**, no valor **product_name**, digite **FreeWheel** (substituindo o conteúdo padrão) e clique em **OK** para fechar a caixa de diálogo **Substituir Parâmetros do Modelo** e modificar o script no Editor de Consultas.  
  
5.  Pressione F5 para executar a consulta, criando o procedimento.  
  
## Próxima tarefa da lição  
[Salvar scripts como projetos ou soluções](../../tools/sql-server-management-studio/save-scripts-as-projects-or-solutions.md)  
  
  
  
