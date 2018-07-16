---
title: Previsão de assistente (Data Mining Add-ins para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84860116150a802648e93686d3e8beb86c4ba037
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323246"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>Assistente de Previsão (Suplementos de Mineração de Dados para Excel)
  ![Assistente para associação na faixa de opções mineração de dados](media/dmc-forecast.gif "Assistente para associação na faixa de opções mineração de dados")  
  
 O assistente de Previsão o ajuda a prever valores em uma série temporal. O assistente de previsão utiliza o algoritmo Série Temporal da [!INCLUDE[msCoName](../includes/msconame-md.md)] ou MTS, que é um algoritmo de regressão para uso na previsão de colunas contínuas, como vendas de produto.  
  
 Cada modelo de previsão deve conter uma série de casos, que é a coluna que faz distinção entre os pontos em uma sequência. Por exemplo, se você estiver usando dados históricos para prever as vendas em um período de vários meses, usará uma coluna contendo uma série de datas como a série de casos.  
  
 Você pode criar previsões de um modelo de previsão sem fornecer novos dados de entrada.  
  
 O [previsão de &#40;ferramentas de análise de tabela para Excel&#41; ](forecast-table-analysis-tools-for-excel.md) ferramenta, o **analisar** faixa de opções, também permite criar modelos de previsão, mas é menos personalizável e só podem usar dados nas tabelas do Excel.  
  
## <a name="using-the-forecast-wizard"></a>Usando o Assistente de Previsão  
  
1.  No **Data Mining** faixa de opções, clique em **previsão**.  
  
2.  No **Selecionar fonte de dados**, escolha a tabela do Excel, intervalo ou fonte de dados externa para usar como entradas.  
  
     Se você usar uma fonte de dados externa, poderá definir a exibição personalizada ou as consultas e salvá-la como uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Sobre o **Forecasting** página, para **carimbo de data / hora**, selecione uma coluna que contém o valor numérico exclusivo (Isso inclui os valores de data e hora) que pode ser usado como a série de casos. A fonte de dados deve ser classificada em ordem crescente por essa coluna.  
  
     Se seus dados não tiverem uma coluna desse tipo, você pode usar a opção \<nenhum carimbo de data / hora >. O assistente adicionará uma coluna de ordem exclusiva para os dados de entrada; em virtude disso, você deverá assegurar que os dados sejam classificados da maneira desejada antes de executar o assistente e escolher essa opção.  
  
4.  Opcionalmente, você pode clicar em **parâmetros** e personalizar o comportamento do modelo de mineração.  
  
     Modelos de previsão dão suporte a vários algoritmos diferentes:  
  
    -   ARIMA  
  
    -   ARTXP (um tipo de modelo de regressão)  
  
    -   ARTXP e ARIMA combinados  
  
     Para obter informações sobre as diferenças, consulte [Microsoft tempo Series Algorithm Technical Reference](data-mining/microsoft-time-series-algorithm-technical-reference.md).  
  
     Você também pode adicionar dicas de periodicidade, especificar opções de atenuação e personalizar opções de regressão para o modelo.  
  
5.  Sobre o **concluir** página, forneça um nome descritivo para o conjunto de dados e o modelo e defina as seguintes opções que controlam como você trabalha com o modelo finalizado:  
  
    -   **Procurar modelo**. Quando essa opção é selecionada, assim que o assistente tiver concluído o processamento do modelo, ele abre uma **procurar** janela para ajudá-lo a explorar os resultados. O conteúdo do visualizador depende do tipo de modelo que você criou. Para obter mais informações, consulte [procurando um modelo de previsão](browsing-a-forecasting-model.md).  
  
    -   **Habilitar o detalhamento**. Selecione esta opção para visualizar os dados subjacentes do modelo finalizado. Essa opção estará disponível somente se você criar um modelo de Árvore de Decisão.  
  
    -   **Usar modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
### <a name="requirements"></a>Requisitos  
 Os dados devem incluir pelo menos uma coluna que possa ser usada como a série temporal. Os valores nesta coluna devem ser exclusivos e contínuos - isto é, não deve haver nenhum intervalo. Antes de executar o assistente, classifique os dados pela coluna da série temporal em ordem crescente.  
  
 Se os dados não incluírem uma coluna de data ou hora, você poderá atribuir uma série numérica arbitrária ou deixar o assistente criar uma. Se você permitir que o assistente crie a coluna da ordem de série, verifique se as outras colunas são classificadas na ordem desejada antes de iniciar o assistente.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Previsão &#40;ferramentas de análise de tabela para Excel&#41;](forecast-table-analysis-tools-for-excel.md)   
 [Procurando um modelo de previsão](browsing-a-forecasting-model.md)  
  
  
