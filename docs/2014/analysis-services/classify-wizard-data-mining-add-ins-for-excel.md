---
title: Assistente de classificação (suplementos de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62d937a733ea41b85a83224a043ff4ad7ecdd29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087927"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>Assistente de Classificação (Suplementos de Mineração de Dados para Excel)
  ![Assistente para Classificação na faixa de opções Mineração de Dados](media/dmc-classify.gif "Assistente para Classificação na faixa de opções Mineração de Dados")  
  
 O assistente de **classificação** ajuda a criar um modelo de classificação com base nos dados existentes em uma tabela do Excel, em um intervalo do Excel ou em uma fonte de dados externa.  
  
 Um modelo de classificação extrai padrões nos dados que indicam similaridades e o ajudam a fazer previsões com base nos agrupamentos de valores. Por exemplo, um modelo de classificação talvez seja usado para prever o risco com base em padrões de renda ou gastos.  
  
## <a name="using-the-classify-wizard"></a>Usando o Assistente para Classificar  
  
1.  Na faixa de faixas de **mineração de dados** , clique em **classificar**e em **Avançar**.  
  
2.  Na página **selecionar dados de origem** , escolha os dados a serem analisados.  
  
     Esse assistente oferece suporte a vários tipos de dados: tabelas do Excel, intervalos do Excel e fontes de dados externas. Com dados externos, você poderá adicioná-la ao Excel ou escolher um conjunto de tabelas ou exibições em uma fonte de dados do Analysis Services. Você também pode adicionar tabelas e alterar colunas para criar fontes de dados ad hoc.  
  
3.  Na página **classificação** , escolha a coluna que você deseja classificar.  
  
     Examine as colunas na lista, **colunas de entrada**e desmarque as colunas que têm valores exclusivos e, portanto, não são úteis para a criação de padrões, como números de ID, nomes de clientes e assim por diante. Você também deve remover colunas que essencialmente duplicam a coluna classificável.  
  
     Por exemplo, se você estiver classificando a previsão da categoria de um produto, deverá excluir o campo da subcategoria se houver uma regra de negócio conhecida, caso contrário, a intensidade dessa regra pode impedir que você descubra outras correlações.  
  
4.  Opcionalmente, clique em **parâmetros** para alterar os parâmetros do algoritmo e personalizar o comportamento do modelo de clustering.  
  
5.  Na página **dividir os dados em conjuntos de treinamento e teste** , especifique a quantidade de dados a serem retidos para teste. O restante é sempre usado para treinar o modelo.  
  
     A configuração padrão é de 30% de dados para teste e 70% de dados para treinamento.  
  
6.  Na página **concluir** , forneça um nome descritivo para seu conjunto de dados e modelo e defina as seguintes opções que controlam como você trabalha com o modelo concluído:  
  
    -   **Procurar modelo**. Quando essa opção é selecionada, assim que o assistente termina de processar o modelo, ele abre uma janela de **procura** para ajudá-lo a explorar os resultados. O conteúdo do visualizador depende do tipo de modelo que você criou. Para obter mais informações, consulte [navegando em um modelo de árvores de decisão](browsing-a-decision-trees-model.md) e [navegando em um modelo de rede neural](browsing-a-neural-network-model.md).  
  
    -   **Habilitar detalhamento**. Selecione esta opção para visualizar os dados subjacentes do modelo finalizado. Essa opção estará disponível somente se você criar um modelo de Árvore de Decisão.  
  
    -   **Use o modelo temporário**. Se você selecionar esta opção, o modelo não será salvo no servidor. Os modelos temporários serão excluídos quando você fechar o Excel.  
  
## <a name="more-about-classification-models"></a>Mais informações sobre os modelos de classificação  
 Na caixa de diálogo **parâmetros de algoritmo** , você também pode escolher o método de classificação entre esses algoritmos fornecidos no Analysis Services:  
  
-   Árvore de Decisão da Microsoft  
  
-   Regressão Logística da Microsoft  
  
-   Microsoft Naïve Bayes  
  
-   Rede Neural da Microsoft  
  
 Embora os algoritmos possam gerar resultados semelhantes, eles analisam os dados de maneira diferente. Portanto, é recomendável tentar vários algoritmos e comparar os resultados. O método padrão é Árvores de Decisão da Microsoft.  
  
 Na lista de **parâmetros** , você pode alterar as opções avançadas, que dependem do tipo de algoritmo escolhido. Os parâmetros para cada algoritmo são descritos mais detalhadamente nos Manuais Online do SQL Server.  
  
 [Referência técnica do algoritmo Árvores de Decisão da Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Regressão Logística da Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Referência técnica do algoritmo Microsoft Naive Bayes](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Microsoft Neural Network Algorithm Technical Reference](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar o assistente de **classificação** , você deve estar conectado a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] um banco de dados. Para obter informações sobre como criar uma conexão, consulte [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)  
  
  
