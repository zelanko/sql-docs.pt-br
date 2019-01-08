---
title: Advanced previsões de série temporal (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b614ebdb-07ca-44af-a0ff-893364bd4b71
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a45d0bf0878b472e4979c00a5a38e8b01974a22
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544334"
---
# <a name="advanced-time-series-predictions-intermediate-data-mining-tutorial"></a>Previsões de série temporal avançadas (Tutorial de mineração de dados intermediário)
  Você viu na exploração do modelo de previsão que embora as vendas na maioria das regiões siga um padrão similar, algumas regiões e alguns modelos, como o M200 na região do Pacífico, exibem tendências muito diferentes. Isso não é surpresa para você, já que sabe que as diferenças entre as regiões são comuns e podem ser causadas por muitos fatores, incluindo promoções de marketing, geração de relatórios imprecisos ou eventos geopolíticos.  
  
 Porém, seus usuários estão pedindo um modelo que possa ser aplicado no mundo todo. Portanto, para minimizar o efeito dos fatores individuais sobre as projeções, você decide criar um modelo baseado em medidas agregadas de vendas mundiais. Assim, você poderá fazer previsões com esse modelo para cada região.  
  
 Nesta tarefa, você criará todas as fontes de dados de que precisa para executar as tarefas de previsão avançadas. Você criará duas exibições de fonte de dados para usar como entradas para a consulta de previsão, e uma exibição de fonte de dados para usar na criação de um novo modelo.  
  
 **Etapas**  
  
1.  [Preparar os dados de vendas estendidos (para previsão)](#bkmk_newExtendData)  
  
2.  [Preparar os dados agregados (para criar o modelo)](#bkmk_newReplaceData)  
  
3.  [Preparar os dados de série (para previsão cruzada)](#bkmk_CrossData2)  
  
4.  [Fazer a previsão usando EXTEND](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
5.  [Criar o modelo de previsão cruzada](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
6.  [Fazer a previsão usando REPLACE](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
7.  [Revisar as novas previsões](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
##  <a name="bkmk_newExtendData"></a> Criando os novos dados de vendas estendidos  
 Para atualizar seus dados de vendas, você precisará obter os números de vendas mais recentes. De interesse em particular são os dados da região do Pacífico, que iniciou uma promoção de vendas regional para chamar a atenção para as novas lojas e aumentar o reconhecimento de seus produtos.  
  
 Para este cenário, vamos supor que os dados importados de uma planilha do Excel que contém apenas três meses de novos dados para duas regiões. Você vai criar uma tabela para os dados usando um script Transact-SQL e, em seguida, definir uma exibição da fonte de dados a ser usado para previsão.  
  
#### <a name="create-the-table-with-new-sales-data"></a>Criar a tabela com os novos dados de vendas  
  
1.  Em uma janela de consulta do Transact-SQL, execute a instrução a seguir para adicionar os dados de vendas ao banco de dados AdventureWorksDW (ou qualquer outro banco de dados).  
  
    ```  
    USE [database name];  
    GO  
    IF OBJECT_ID ([dbo].[NewSalesData]) IS NOT NULL   
        DROP TABLE [dbo].[NewSalesData];  
    GO  
    CREATE TABLE [dbo].[NewSalesData]([Series] [nvarchar](255) NULL,  
    [NewDate] [datetime] NULL,  
    [NewQty] [float] NULL,  
    [NewAmount] [money] NULL) ON [PRIMARY]  
  
    GO  
    ```  
  
2.  Insira os novos valores usando o script a seguir.  
  
    ```  
    INSERT INTO [NewSalesData]  
    (Series,NewDate,NewQty,NewAmount)  
    VALUES('T1000 Pacific', '7/25/08', 55, '$130,170.22'),  
    ('T1000 Pacific', '8/25/08', 50, '$114,435.36 '),  
    ('T1000 Pacific', '9/25/08', 50, '$117,296.24 '),  
    ('T1000 Europe', '7/25/08', 37, '$88,210.00 '),  
    ('T1000 Europe', '8/25/08', 41, '$97,746.00 '),  
    ('T1000 Europe', '9/25/08', 37, '$88,210.00 '),  
    ('T1000 North America', '7/25/08', 69, '$164,500.00 '),  
    ('T1000 North America', '8/25/08', 66, '$157,348.00 '),  
    ('T1000 North America', '9/25/08', 58, '$138,276.00 '),  
    ('M200 Pacific', '7/25/08', 65, '$149,824.35'),  
    ('M200 Pacific', '8/25/08', 54,  '$124,619.46'),  
    ('M200 Pacific', '9/25/08', 61, '$141,143.39'),  
    ('M200 Europe', '7/25/08', 75, '$173,026.00'),  
    ('M200 Europe', '8/25/08', 76, '$175,212.00'),  
    ('M200 Europe', '9/25/08', 84, '$193,731.00'),  
    ('M200 North America', '7/25/08', 94, '$216,916.00'),  
    ('M200 North America', '8/25/08', 94, '$216,891.00'),  
    ('M200 North America', '9/25/08', 91,'$209,943.00');  
    ```  
  
    > [!WARNING]  
    >  Os aspas são usadas com os valores de moeda para evitar problemas com o separador de vírgula e o símbolo de moeda. Você também pode transmitir os valores de moeda neste formato: `130170.22`  
    >   
    >  Observe que as datas usadas no banco de dados de exemplo foram alteradas para esta versão. Se você estiver usando uma edição anterior do AdventureWorks, poderá precisar ajustar as datas inseridas de acordo.  
  
###  <a name="bkmk_newReplaceData"></a> Criar uma exibição da fonte de dados usando os novos dados de vendas  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **exibições da fonte de dados**e, em seguida, selecione **nova exibição da fonte de dados**.  
  
2.  No Assistente de Exibição da Fonte de Dados, faça as seguintes seleções:  
  
     **Fonte de dados**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Selecionar tabelas e exibições**: Selecione a tabela que você acabou de criar NewSalesData.  
  
3.  Clique em **Concluir**.  
  
4.  Na superfície de design de exibição da fonte de dados, NewSalesData com o botão direito e, em seguida, selecione **explorar dados** para verificar os dados.  
  
> [!WARNING]  
>  Você usará estes dados somente para previsão. Portanto, não importa se os dados estão incompletos.  
  
##  <a name="bkmk_CrossData2"></a> Criando os dados para o modelo de previsão cruzada  
 Os dados que foi usados no original previsão de modelo já estava agrupados de certa forma, a exibição vTimeSeries, recolhidas vários modelos de bicicleta em um número menor de categorias e mesclou os resultados de países individuais em regiões. Para criar um modelo que possa ser usado para projeções mundiais, você criará mais algumas agregações simples diretamente no Designer de Exibição da Fonte de Dados. A nova exibição da fonte de dados contém apenas a soma e a média das vendas de todos os produtos para todas as regiões.  
  
 Depois de criar a fonte de dados usada no modelo, você deve criar uma nova exibição da fonte de dados para usar na previsão. Por exemplo, se você desejar prever vendas para a Europa usando o novo modelo mundial, deverá preencher os dados somente para a região da Europa. Dessa forma, você definirá uma nova exibição de fonte de dados que filtra os dados originais, e alterará a condição de filtro para cada conjunto de consultas de previsão.  
  
#### <a name="to-create-the-model-data-using-a-custom-data-source-view"></a>Para criar os dados do modelo usando uma exibição de fonte de dados personalizada  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **exibições da fonte de dados**e, em seguida, selecione **nova exibição da fonte de dados**.  
  
2.  Na página de boas-vindas do assistente, clique em **Avançar**.  
  
3.  Na página **Selecionar Fonte de Dados** , selecione [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]e, em seguida, clique em **Avançar**.  
  
4.  Na página de **selecionar tabelas e exibições**, não adicione qualquer clique apenas em tabelas **próxima**.  
  
5.  Na página de **Concluindo o assistente**, digite o nome `AllRegions`e, em seguida, clique em **concluir**.  
  
6.  Em seguida, clique com botão direito a superfície de design de exibição da fonte de dados em branco e, em seguida, selecione **nova consulta nomeada**.  
  
7.  No **criar consulta nomeada** caixa de diálogo, para **nome**, tipo `AllRegions`e para **descrição**, tipo **soma e média de vendas para todos os modelos e regiões**.  
  
8.  No painel de texto do SQL, digite a seguinte instrução e clique em OK:  
  
    ```  
    SELECT ReportingDate,   
    SUM([Quantity]) as SumQty, AVG([Quantity]) as AvgQty,  
    SUM([Amount]) AS SumAmt, AVG([Amount]) AS AvgAmt,  
    'All Regions' as [Region]  
    FROM dbo.vTimeSeries   
    GROUP BY ReportingDate  
    ```  
  
9. Clique com botão direito do `AllRegions` de tabela e, em seguida, selecione **explorar dados**.  
  
###  <a name="bkmk_CrossData"></a> Para criar os dados de série para previsão cruzada  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **exibições da fonte de dados**e, em seguida, selecione **nova exibição da fonte de dados**.  
  
2.  No Assistente de Exibição da Fonte de Dados, faça as seguintes seleções:  
  
     **Fonte de dados**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Selecionar tabelas e exibições**: Não selecione nenhuma tabela  
  
     **Nome**: `T1000 Pacific Region`  
  
3.  Clique em **Concluir**.  
  
4.  A superfície de design vazio para o botão direito do mouse **T1000 Pacific Region**e, em seguida, selecione **nova consulta nomeada**.  
  
     A caixa de diálogo **Criar Consulta Nomeada** é aberta. Digite o nome novamente e, em seguida, adicione a seguinte descrição:  
  
     **Nome**: `T1000 Pacific Region`  
  
     **Descrição**: **Filtro`vTimeSeries`por região e modelo**  
  
5.  No painel de texto, digite a seguinte consulta e clique em OK:  
  
    ```  
    SELECT ReportingDate, ModelRegion, Quantity, Amount  
    FROM dbo.vTimeSeries  
    WHERE (ModelRegion = N'T1000 Pacific')  
    ```  
  
    > [!NOTE]  
    >  Como você precisará criar previsões para cada série separadamente, talvez você queira copiar o texto da consulta e salvá-lo em um arquivo de texto para que seja possível reutilizá-lo na outra série de dados.  
  
6.  Na superfície de design de exibição da fonte de dados, clique com botão direito T1000 Pacific e, em seguida, selecione **explorar dados** para verificar se os dados foram filtrados corretamente.  
  
     Você usará esses dados como a entrada para o modelo ao criar consultas da previsão cruzada.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Usando dados atualizados de previsões de série temporal &#40;Tutorial intermediário de mineração de dados&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmo MTS](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Referência técnica do algoritmo MTS](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Exibições de fontes de dados em modelos multidimensionais](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
