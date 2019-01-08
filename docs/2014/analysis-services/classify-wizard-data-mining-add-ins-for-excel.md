---
title: Classificar o Assistente (Data Mining Add-ins para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9109f47ba1173c115234f9040445fb110e3f0e3c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419677"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>Assistente de Classificação (Suplementos de Mineração de Dados para Excel)
  ![Assistente de classificar na faixa de opções mineração de dados](media/dmc-classify.gif "Assistente classificar na faixa de opções mineração de dados")  
  
 O **classificar** assistente o ajuda a criar um modelo de classificação com base nos dados existentes em uma tabela do Excel, um intervalo do Excel ou uma fonte de dados externa.  
  
 Um modelo de classificação extrai padrões nos dados que indicam similaridades e o ajudam a fazer previsões com base nos agrupamentos de valores. Por exemplo, um modelo de classificação talvez seja usado para prever o risco com base em padrões de renda ou gastos.  
  
## <a name="using-the-classify-wizard"></a>Usando o Assistente para Classificar  
  
1.  No **Data Mining** faixa de opções, clique em **classificar**e, em seguida, clique em **próxima**.  
  
2.  No **Selecionar fonte de dados** , escolha os dados a serem analisados.  
  
     Esse assistente oferece suporte a vários tipos de dados: Tabelas do Excel, intervalos do Excel e fontes de dados externas. Com dados externos, você poderá adicioná-la ao Excel ou escolher um conjunto de tabelas ou exibições em uma fonte de dados do Analysis Services. Você também pode adicionar tabelas e alterar colunas para criar fontes de dados ad hoc.  
  
3.  Sobre o **classificação** página, escolha a coluna que você deseja classificar.  
  
     Revise as colunas na lista, **colunas de entrada**e desmarque as colunas que têm valores exclusivos e, portanto, não são úteis para a criação de padrões, como números de identificação, nomes de cliente e assim por diante. Você também deve remover colunas que essencialmente duplicam a coluna classificável.  
  
     Por exemplo, se você estiver classificando a previsão da categoria de um produto, deverá excluir o campo da subcategoria se houver uma regra de negócio conhecida, caso contrário, a intensidade dessa regra pode impedir que você descubra outras correlações.  
  
4.  Opcionalmente, clique em **parâmetros** para alterar os parâmetros de algoritmo e personalizar o comportamento do modelo de clustering.  
  
5.  No **dividir dados em conjuntos de teste e treinamento** , especifique a quantidade de dados será mantida para teste. O restante é sempre usado para treinar o modelo.  
  
     A configuração padrão é de 30% de dados para teste e 70% de dados para treinamento.  
  
6.  Sobre o **concluir** página, forneça um nome descritivo para o conjunto de dados e o modelo e defina as seguintes opções que controlam como você trabalha com o modelo finalizado:  
  
    -   **Procurar modelo**. Quando essa opção é selecionada, assim que o assistente tiver concluído o processamento do modelo, ele abre uma **procurar** janela para ajudá-lo a explorar os resultados. O conteúdo do visualizador depende do tipo de modelo que você criou. Para obter mais informações, consulte [procurando um modelo de árvores de decisão](browsing-a-decision-trees-model.md) e [procurando um modelo de rede Neural](browsing-a-neural-network-model.md).  
  
    -   **Habilitar o detalhamento**. Selecione esta opção para visualizar os dados subjacentes do modelo finalizado. Essa opção estará disponível somente se você criar um modelo de Árvore de Decisão.  
  
    -   **Usar modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
## <a name="more-about-classification-models"></a>Mais informações sobre os modelos de classificação  
 No **parâmetros de algoritmo** caixa de diálogo, você também pode escolher o método de classificação entre esses algoritmos fornecidos no Analysis Services:  
  
-   Árvore de Decisão da Microsoft  
  
-   Regressão Logística da Microsoft  
  
-   Microsoft Naïve Bayes  
  
-   Rede Neural da Microsoft  
  
 Embora os algoritmos possam gerar resultados semelhantes, eles analisam os dados de maneira diferente. Portanto, é recomendável tentar vários algoritmos e comparar os resultados. O método padrão é Árvores de Decisão da Microsoft.  
  
 No **parâmetros** lista, você pode alterar as opções avançadas, que dependem do tipo de algoritmo escolhido. Os parâmetros para cada algoritmo são descritos mais detalhadamente nos Manuais Online do SQL Server.  
  
 [Referência técnica do algoritmo Árvores de Decisão da Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Regressão Logística da Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Microsoft Naive Bayes](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Rede Neural da Microsoft](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar o **classificar** assistente, você deve estar conectado a um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados. Para obter informações sobre como criar uma conexão, consulte [conectar-se a fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)  
  
  
