---
title: Assistente de previsão (suplementos de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
author: minewiskan
ms.author: owend
ms.openlocfilehash: d3c4d728f810da7abf96d1addc6ef91156a3d5ea
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544418"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>Assistente de Previsão (Suplementos de Mineração de Dados para Excel)
  ![Assistente para Associação na faixa de opções Mineração de Dados](media/dmc-forecast.gif "Assistente para Associação na faixa de opções Mineração de Dados")  
  
 O assistente de Previsão o ajuda a prever valores em uma série temporal. O assistente de previsão utiliza o algoritmo Série Temporal da [!INCLUDE[msCoName](../includes/msconame-md.md)] ou MTS, que é um algoritmo de regressão para uso na previsão de colunas contínuas, como vendas de produto.  
  
 Cada modelo de previsão deve conter uma série de casos, que é a coluna que faz distinção entre os pontos em uma sequência. Por exemplo, se você estiver usando dados históricos para prever as vendas em um período de vários meses, usará uma coluna contendo uma série de datas como a série de casos.  
  
 Você pode criar previsões de um modelo de previsão sem fornecer novos dados de entrada.  
  
 A [previsão &#40;ferramentas de análise de tabela para&#41;](forecast-table-analysis-tools-for-excel.md) ferramenta do Excel, na faixa de quadro **analisar** , também permite que você crie modelos de previsão, mas é menos personalizável e só pode usar dados em tabelas do Excel.  
  
## <a name="using-the-forecast-wizard"></a>Usando o Assistente de Previsão  
  
1.  Na faixa de faixas de **mineração de dados** , clique em **previsão**.  
  
2.  Em **selecionar dados de origem**, escolha a tabela do Excel, o intervalo ou a fonte de dados externa para usar como entradas.  
  
     Se você usar uma fonte de dados externa, poderá definir a exibição personalizada ou as consultas e salvá-la como uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Na página **previsão** , para carimbo de data/ **hora**, selecione uma coluna que contenha um valor numérico exclusivo (isso inclui valores de dados e de hora) que podem ser usados como a série de casos. A fonte de dados deve ser classificada em ordem crescente por essa coluna.  
  
     Se os dados não tiverem essa coluna, você poderá usar a opção \<no time stamp> . O assistente adicionará uma coluna de ordem exclusiva para os dados de entrada; em virtude disso, você deverá assegurar que os dados sejam classificados da maneira desejada antes de executar o assistente e escolher essa opção.  
  
4.  Opcionalmente, você pode clicar em **parâmetros** e personalizar o comportamento do modelo de mineração.  
  
     Modelos de previsão dão suporte a vários algoritmos diferentes:  
  
    -   ARIMA  
  
    -   ARTXP (um tipo de modelo de regressão)  
  
    -   ARTXP e ARIMA combinados  
  
     Para obter informações sobre as diferenças, consulte [referência técnica do algoritmo do Microsoft Time Series](data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
     Você também pode adicionar dicas de periodicidade, especificar opções de atenuação e personalizar opções de regressão para o modelo.  
  
5.  Na página **concluir** , forneça um nome descritivo para seu conjunto de dados e modelo e defina as seguintes opções que controlam como você trabalha com o modelo concluído:  
  
    -   **Procurar modelo**. Quando essa opção é selecionada, assim que o assistente termina de processar o modelo, ele abre uma janela de **procura** para ajudá-lo a explorar os resultados. O conteúdo do visualizador depende do tipo de modelo que você criou. Para obter mais informações, consulte [navegando em um modelo de previsão](browsing-a-forecasting-model.md).  
  
    -   **Habilitar detalhamento**. Selecione esta opção para visualizar os dados subjacentes do modelo finalizado. Essa opção estará disponível somente se você criar um modelo de Árvore de Decisão.  
  
    -   **Use o modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
### <a name="requirements"></a>Requisitos  
 Os dados devem incluir pelo menos uma coluna que possa ser usada como a série temporal. Os valores nesta coluna devem ser exclusivos e contínuos, ou seja, não deve haver intervalos. Antes de executar o assistente, classifique os dados pela coluna da série temporal em ordem crescente.  
  
 Se os dados não incluírem uma coluna de data ou hora, você poderá atribuir uma série numérica arbitrária ou deixar o assistente criar uma. Se você permitir que o assistente crie a coluna da ordem de série, verifique se as outras colunas são classificadas na ordem desejada antes de iniciar o assistente.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Previsão de &#40;ferramentas de análise de tabela para Excel&#41;](forecast-table-analysis-tools-for-excel.md)   
 [Procurando um modelo de previsão](browsing-a-forecasting-model.md)  
  
  
