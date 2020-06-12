---
title: 'Lição 11: criar partições | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 545c6f45339047d3a632f9e18d69108f3c8b5111
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543578"
---
# <a name="lesson-11-create-partitions"></a>Lição 11: Criar partições
  Nesta lição, você criará partições para dividir a tabela Internet Sales em partes lógicas menores que podem ser processadas (Atualizadas) independentemente de outras partições. Por padrão, cada tabela que você inclui em seu modelo tem uma partição que inclui todas as colunas e linhas da tabela. Para a tabela vendas pela Internet, desejamos dividir os dados por ano; uma partição para cada um dos cinco anos da tabela.  Cada partição pode ser processada independentemente. Para obter mais informações, consulte [Partições &#40;SSAS Tabular&#41;](tabular-models/partitions-ssas-tabular.md).  
  
 Tempo estimado para conclusão desta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de realizar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 10: Criar hierarquias](lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Criar partições  
  
#### <a name="to-create-partitions-in-the-internet-sales-table"></a>Para criar partições na tabela Internet Sales  
  
1.  No designer de modelos, clique na tabela **Internet Sales** , clique no menu **Tabela** e em **Partições**.  
  
     A caixa de diálogo **Gerenciador de Partições** é aberta.  
  
2.  Na caixa de diálogo **Gerenciador de partições** , em **partições**, clique na partição **Internet Sales** .  
  
3.  Em **nome da partição**, altere o nome para `Internet Sales 2005` .  
  
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
  
     Observe que um aviso é exibido, declarando que determinadas colunas não estão presentes na origem. Isso ocorre porque, na [lição 3: renomear colunas](rename-columns.md), você renomeou essas colunas na tabela vendas pela Internet no modelo para serem diferentes daquelas mesmas colunas na origem.  
  
#### <a name="to-create-a-partition-for-the-2006-year-in-the-internet-sales-table"></a>Para criar uma partição para o ano de 2006 na tabela vendas pela Internet  
  
1.  Na caixa de diálogo **Gerenciador de partições** , em **partições**, clique na `Internet Sales 2005` partição que você acabou de criar e, em seguida, **Copie**.  
  
2.  Em **nome da partição**, digite `Internet Sales 2006` .  
  
3.  Na instrução SQL, para que a partição inclua somente as linhas do ano 2006, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2006-01-01 00:00:00') AND ([OrderDate] < N'2007-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2007-year-in-the-internet-sales-table"></a>Para criar uma partição para o ano de 2007 na tabela vendas pela Internet  
  
1.  Na caixa de diálogo **Gerenciador de Partições** , clique em **Copiar**.  
  
2.  Em **nome da partição**, digite `Internet Sales 2007` .  
  
3.  Em **alternar para**, selecione **Editor de consultas**.  
  
4.  Na instrução SQL, para que a partição inclua somente as linhas do ano 2007, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2007-01-01 00:00:00') AND ([OrderDate] < N'2008-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2008-year-in-the-internet-sales-table"></a>Para criar uma partição para o ano de 2008 na tabela vendas pela Internet  
  
1.  Na caixa de diálogo **Gerenciador de Partições** , clique em **Novo**.  
  
2.  Em **nome da partição**, digite `Internet Sales 2008` .  
  
3.  Em **alternar para**, selecione **Editor de consultas**.  
  
4.  Na instrução SQL, para que a partição inclua somente as linhas do ano 2008, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2008-01-01 00:00:00') AND ([OrderDate] < N'2009-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2009-year-in-the-internet-sales-table"></a>Para criar uma partição para o ano 2009 na tabela Internet Sales  
  
1.  Na caixa de diálogo **Gerenciador de Partições** , clique em **Novo**.  
  
2.  Em **nome da partição**, digite `Internet Sales 2009` .  
  
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
  
4.  Selecione a caixa de seleção na coluna **Processo** para cada uma das cinco partições criadas e depois clique em **OK**.  
  
     Se você for solicitado a fornecer credenciais de Representação, insira o nome de usuário e a senha do Windows que especificou na Lição 2, etapa 6.  
  
     A caixa de diálogo **processo de dados** é exibida e exibe os detalhes do processo para cada partição. Observe que um número diferente de linhas para cada partição é transferido. Isso acontece porque cada partição inclui somente as linhas referentes ao ano especificado na cláusula WHERE da Instrução SQL: Não há nenhum dado para o ano 2010.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 12: Criar funções](lesson-11-create-roles.md).  
  
  
