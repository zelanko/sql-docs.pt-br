---
title: "Lição 11: Criar partições | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57ed4f364bcc7ca144c6e963c7b550a5dcc1831d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-10-create-partitions"></a>Lição 10: Criar partições
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará partições dividir a tabela FactInternetSales em partes lógicas menores que podem ser processadas (atualizadas) independentemente de outras partições. Por padrão, cada tabela que você inclui no modelo tem uma partição que contém todas as colunas e linhas da tabela. Para a tabela FactInternetSales, desejamos dividir os dados por ano; uma partição para cada um dos cinco anos da tabela. Cada partição pode ser processada independentemente. Para obter mais informações, consulte [Partições](../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 9: criar hierarquias](../analysis-services/lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Criar partições  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Para criar partições na tabela FactInternetSales  
  
1.  No Gerenciador de modelos tabulares, expanda **tabelas**, clique com botão direito **FactInternetSales** > **partições**.  
  
2.  Na caixa de diálogo Gerenciador de partições, clique em **cópia**.  
  
3.  Em **nome da partição**, altere o nome para **FactInternetSales2010**.  
  
    > [!TIP]  
    > Observe os nomes das colunas na janela de visualização de tabela exibem essas colunas incluídas na tabela de modelo (marcada) com os nomes de coluna da origem. Isso acontece porque a janela Visualização de Tabela exibe colunas da tabela de origem, e não da tabela de modelo.  
  
4.  Selecione o **SQL** botão logo acima do lado direito da janela de visualização para abrir o editor de instrução SQL.  
  
    Como você deseja que a partição inclua apenas essas linhas em um certo período, você deve incluir uma cláusula WHERE. Você só pode criar uma cláusula WHERE usando uma Instrução SQL.  
  
5.  No **instrução SQL** campo, substitua a instrução existente, copiando e colando a seguinte instrução:  
  
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
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    Essa instrução especifica que a partição deve incluir todos os dados nas linhas em que OrderDate se refere ao ano civil 2010, conforme especificado na cláusula WHERE.  
  
6.  Clique em **Validar**.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>Para criar uma partição para o ano 2011  
  
1.  Na lista de partições, clique no **FactInternetSales2010** partição que você acabou de criar e, em seguida, clique em **cópia**.  
  
2.  Em **nome da partição**, tipo **FactInternetSales2011**.  
  
3.  Na Instrução SQL, para que a partição inclua somente as linhas do ano 2011, substitua a cláusula WHERE pelo seguinte:  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2012-year"></a>Para criar uma partição para o ano 2012  
  
- Siga as etapas acima, usando a seguinte cláusula WHERE. 
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2013-year"></a>Para criar uma partição para o ano 2013  
  
- Siga as etapas acima, usando a seguinte cláusula WHERE. 
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2014-year"></a>Para criar uma partição para o ano de 2014  
  
- Siga as etapas acima, usando a seguinte cláusula WHERE. 
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  

## <a name="delete-the-factinternetsales-partition"></a>Excluir a partição FactInternetSales
Agora que você tiver partições para cada ano, você pode excluir a partição FactInternetSales. Isso impede que se sobrepõem ao escolher o processo de todos os durante o processamento de partições.
#### <a name="to-delete-the-factinternetsales-partition"></a>Para excluir a partição FactInternetSales
-  Clique na partição FactInternetSales e, em seguida, clique em **excluir**.



## <a name="process-partitions"></a>Processar partições  
No Gerenciador de partições, observe o **último processados** coluna para cada um dos novos partições acabou de criar mostra essas partições nunca tiveram sido processadas. Quando você cria novas partições, deve executar a operação Processar Partições ou Processar Tabela para atualizar os dados nessas partições.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>Para processar as partições de FactInternetSales  
  
1.  Clique em **Okey** para fechar a caixa de diálogo Gerenciador de partições.  
  
2.  Clique o **FactInternetSales** de tabela e, em seguida, clique no **modelo** menu > **processo** > **processar partições**.  
  
3.  Na caixa de diálogo processar partições, verifique se **modo** é definido como **processar padrão**.  
  
4.  Marque a caixa de seleção na coluna **Processar** para cada uma das cinco partições criadas e clique em **OK**.  

    ![como--lesson10-processo-partições de tabela](../analysis-services/media/as-tabular-lesson10-process-partitions.png)
  
    Se você for solicitado a fornecer credenciais de representação, insira o nome de usuário do Windows e a senha que você especificou na lição 2.  
  
    A caixa de diálogo **Processamento de Dados** será exibida, mostrando os detalhes do processo de cada partição. Observe que um número diferente de linhas para cada partição é transferido. Isso acontece porque cada partição inclui somente as linhas referentes ao ano especificado na cláusula WHERE da Instrução SQL: Quando o processamento for concluído, vá em frente e feche a caixa de diálogo Processamento de Dados.  
  
    ![como-tabela-lesson10-processo-concluído](../analysis-services/media/as-tabular-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 11: criar funções](../analysis-services/lesson-11-create-roles.md). 

