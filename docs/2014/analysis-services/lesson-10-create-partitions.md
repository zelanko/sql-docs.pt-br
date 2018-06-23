---
title: 'Lição 11: Criar partições | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: c480583da42aee4f73e6053d20e7bf8b6542547c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009866"
---
# <a name="lesson-11-create-partitions"></a>Lição 11: Criar partições
  Nesta lição, você criará partições para dividir a tabela Internet Sales em partes lógicas menores que podem ser processadas (Atualizadas) independentemente de outras partições. Por padrão, cada tabela que você inclui no modelo tem uma partição que contém todas as colunas e linhas da tabela. No caso da tabela Internet Sales, desejamos dividir os dados por ano; uma partição para cada um dos cinco anos da tabela.  Cada partição pode ser processada independentemente. Para obter mais informações, consulte [Partições &#40;SSAS Tabular&#41;](tabular-models/partitions-ssas-tabular.md).  
  
 Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 10: Criar hierarquias](lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Criar partições  
  
#### <a name="to-create-partitions-in-the-internet-sales-table"></a>Para criar partições na tabela Internet Sales  
  
1.  No designer de modelos, clique na tabela **Internet Sales** , clique no menu **Tabela** e em **Partições**.  
  
     A caixa de diálogo **Gerenciador de Partições** é aberta.  
  
2.  No **Gerenciador de partições** na caixa **partições**, clique no **vendas pela Internet** partição.  
  
3.  Em **nome da partição**, altere o nome para `Internet Sales 2005`.  
  
    > [!TIP]  
    >  Antes de passar para a próxima etapa, observe que os nomes de coluna na janela Visualização de Tabela exibem essas colunas incluídas na tabela de modelo (marcada) com os nomes de coluna da origem. Isso acontece porque a janela Visualização de Tabela exibe colunas da tabela de origem, e não da tabela de modelo.  
  
4.  Selecione o botão **Editor de Consultas** logo acima do lado direito da janela de visualização.  
  
     Como você deseja que a partição inclua apenas essas linhas em um certo período, você deve incluir uma cláusula WHERE. Você só pode criar uma cláusula WHERE usando uma Instrução SQL.  
  
5.  No campo **Instrução SQL** , substitua a instrução existente colando a seguinte instrução:  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2005-01-01 00:00:00') AND ([OrderDate] < N'2006-01-01 00:00:00'))  
    ```  
  
     Essa instrução especifica que a partição deve incluir todos os dados nas linhas onde OrderDate refere-se ao ano civil 2005 conforme especificado na cláusula WHERE.  
  
6.  Clique em **Validar**.  
  
     Observe que um aviso é exibido, declarando que determinadas colunas não estão presentes na origem. Isso ocorre porque no [lição 3: renomear colunas](rename-columns.md), você renomeou essas colunas na tabela de vendas pela Internet no modelo a ser diferentes das mesmas colunas na origem.  
  
#### <a name="to-create-a-partition-for-the-2006-year-in-the-internet-sales-table"></a>Para criar uma partição do ano 2006 na tabela de vendas pela Internet  
  
1.  No **Gerenciador de partições** na caixa **partições**, clique no `Internet Sales 2005` partição que você acabou de criar e, em seguida, **cópia**.  
  
2.  Em **nome da partição**, tipo `Internet Sales 2006`.  
  
3.  Na instrução SQL, em ordem para a partição inclua somente as linhas para o ano de 2006, substitua a cláusula WHERE com o seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2006-01-01 00:00:00') AND ([OrderDate] < N'2007-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2007-year-in-the-internet-sales-table"></a>Para criar uma partição para o ano de 2007 na tabela de vendas pela Internet  
  
1.  Na caixa de diálogo **Gerenciador de Partições** , clique em **Copiar**.  
  
2.  Em **nome da partição**, tipo `Internet Sales 2007`.  
  
3.  Em **alternar para**, selecione **Editor de consultas**.  
  
4.  Na instrução SQL, em ordem para a partição inclua somente as linhas para o ano de 2007, substitua a cláusula WHERE com o seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2007-01-01 00:00:00') AND ([OrderDate] < N'2008-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2008-year-in-the-internet-sales-table"></a>Para criar uma partição para o ano de 2008 na tabela de vendas pela Internet  
  
1.  Na caixa de diálogo **Gerenciador de Partições** , clique em **Novo**.  
  
2.  Em **nome da partição**, tipo `Internet Sales 2008`.  
  
3.  Em **alternar para**, selecione **Editor de consultas**.  
  
4.  Na instrução SQL, em ordem para a partição inclua somente as linhas para o ano de 2008, substitua a cláusula WHERE com o seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2008-01-01 00:00:00') AND ([OrderDate] < N'2009-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2009-year-in-the-internet-sales-table"></a>Para criar uma partição para o ano 2009 na tabela Internet Sales  
  
1.  Na caixa de diálogo **Gerenciador de Partições** , clique em **Novo**.  
  
2.  Em **nome da partição**, tipo `Internet Sales 2009`.  
  
3.  Em **alternar para**, selecione **Editor de consultas**.  
  
4.  Na Instrução SQL, para que a partição inclua somente as linhas do ano 2009, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2009-01-01 00:00:00') AND ([OrderDate] < N'2010-01-01 00:00:00'))  
    ```  
  
## <a name="process-partitions"></a>Processar partições  
 Na caixa de diálogo **Gerenciador de Partições** , observe o asterisco (**\***) ao lado dos nomes de partição de cada nova partição que você acabou de criar. Isso indica que a partição não foi processada (atualizada). Quando você cria novas partições, deve executar a operação Processar Partições ou Processar Tabela para atualizar os dados nessas partições.  
  
#### <a name="to-process-internet-sales-partitions"></a>Para processar partições Internet Sales  
  
1.  Clique em **OK** para fechar a caixa de diálogo **Gerenciador de Partições** .  
  
2.  No designer de modelos, clique na tabela **Internet Sales** , clique no menu **Modelo** , aponte para **Processar** (Atualizar) e clique em **Processar Partições**.  
  
3.  Na caixa de diálogo **Processar Partições** , verifique se o **Modo** está definido como **Processo Padrão**.  
  
4.  Marque a caixa de seleção na coluna **Processar** para cada uma das cinco partições criadas e clique em **OK**.  
  
     Se você for solicitado a fornecer credenciais de Representação, insira o nome de usuário e a senha do Windows que especificou na Lição 2, etapa 6.  
  
     O **processo dados** caixa de diálogo, em seguida, aparece e exibe os detalhes do processo para cada partição. Observe que um número diferente de linhas para cada partição é transferido. Isso acontece porque cada partição inclui somente as linhas referentes ao ano especificado na cláusula WHERE da Instrução SQL: Não há nenhum dado para o ano 2010.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 12: Criar funções](lesson-11-create-roles.md).  
  
  