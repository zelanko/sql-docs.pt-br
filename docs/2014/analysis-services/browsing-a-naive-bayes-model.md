---
title: Navegando em um modelo de Bayes Naive | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b8bb26a72903644b5985d69efc8adb362fe412
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088477"
---
# <a name="browsing-a-naive-bayes-model"></a>Procurando um modelo Naive Bayes
  Quando você abre um modelo Bayes simples usando **procurar**, o modelo é exibido em um visualizador interativo com quatro painéis diferentes. Use o visualizador para explorar correlações e obter informações sobre o modelo e os dados subjacentes.  
  
-   [Rede de dependências](#bkmk_DepNet)  
  
-   [Perfis de atributo](#bkmk_AttProf)  
  
-   [Características do atributo](#bkmk_AttChar)  
  
-   [Discriminação de atributo](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a>Explorar o modelo  
 A finalidade do visualizador é ajudar a explorar a interação entre os atributos de entrada e saída (entradas e variáveis dependentes) que foram descobertos pelo modelo Naïve Bayes da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Se você quiser experimentar o Bayes Viewer do ingênua, use o [Assistente para classificar &#40;suplementos de mineração de dados para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md) na faixa de opções mineração de dados, clique na opção **avançado** e altere o algoritmo para usar o algoritmo de Bayes ingênua  
  
 Para esses exemplos, usamos os dados de origem na pasta de trabalho de exemplo e agrupamos a coluna, **renda anual**, em cinco grupos de renda, de **muito baixo** para **muito alto**. O modelo Naïve Bayes analisou os fatores correlacionadas com cada categoria de renda.  
  
###  <a name="bkmk_DepNet"></a>Rede de dependências  
 A primeira janela que você usará é a **rede de dependência**. Ela mostra uma visão geral cujas entradas estão estreitamente correlacionadas ao resultado selecionado.  
  
 ![rede de dependências no Visualizador Naive Bayes](media/dm13-nb.gif "rede de dependências no Visualizador Naive Bayes")  
  
##### <a name="explore-the-dependency-network"></a>Explorar a rede de dependências  
  
1.  Primeiro, clique no resultado de destino, **renda anual**, que é representado como um nó no grafo.  
  
     Os nós realçados em volta da variável pretendida são os que estão correlacionadas estatisticamente com esse resultado. Use a legenda na parte inferior do visualizador para entender a natureza da relação.  
  
2.  Clique no controle deslizante à esquerda do visualizador e arraste-o para baixo.  
  
     Esse controle filtra as variáveis independentes, com base nos pontos fortes das dependências. Quando você arrasta o controle deslizante para baixo, apenas os links mais importantes permanecem no gráfico.  
  
3.  Depois de filtrar o grafo, clique no botão **copiar exibição de gráfico**. Selecione uma planilha do Excel e pressione Ctrl+V.  
  
     Essa opção copia a exibição selecionada, inclusive filtros e realce.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a>Perfis de atributo  
 As janelas de **perfis de atributo** proporcionam a você uma indicação visual de como todas as outras variáveis estão relacionadas aos resultados individuais.  
  
##### <a name="explore-the-profiles"></a>Explorar os perfis  
  
1.  Para ocultar alguns valores para que você possa comparar resultados mais facilmente, clique no título da coluna e arraste-o para baixo de outra coluna.  
  
     ![perfis de atributos no Visualizador Naive Bayes](media/dm13-nb-attprof.gif "perfis de atributos no Visualizador Naive Bayes")  
  
2.  Clique em qualquer célula para exibir a distribuição de valores na **legenda de mineração**.  
  
     Como os atributos associados a resultados diferentes são exibidos visualmente, é fácil reconhecer correlações interessantes, por exemplo, como as rendas são distribuídas por região.  
  
3.  Para obter os dados subjacentes a essa exibição, clique em **copiar para o Excel**. Uma tabela é gerada em uma nova planilha que mostra as correlações entre atributos individuais e resultados. Nessa tabela do Excel, você pode facilmente ocultar ou filtrar colunas.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a>Características do atributo  
 A exibição de **características de atributo** é útil para o exame detalhado de uma variável de resultado específica e os fatores de contribuição.  
  
 ![características de atributos no Visualizador Naive Bayes](media/dm13-nb-viewer.gif "características de atributos no Visualizador Naive Bayes")  
  
##### <a name="explore-the-attribute-characteristics"></a>Explorar as características do atributo  
  
1.  Clique em **valor** e selecione um item do **valor**.  
  
     Quando você selecionar um resultado pretendido, o gráfico será atualizado para mostrar os fatores que estão mais fortemente associados ao resultado, classificados por importância.  
  
     Observe que se você criar um modelo usando a opção [analisar influenciadores de chave &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md) , poderá criar modelos que tenham mais de um atributo previsível. No entanto, todos os outros assistentes nos suplementos de Mineração de Dados limitam a um atributo previsível.  
  
2.  Clique em **copiar para o Excel** para criar uma tabela, em uma nova planilha, listando as pontuações de todos os atributos relacionados ao resultado de destino selecionado.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a>Discriminação de atributo  
 A exibição de **discriminação de atributo** ajuda a comparar dois resultados, ou um resultado versus todos os outros resultados.  
  
 ![discriminação de atributos no Visualizador Naive Bayes](media/dm13-nb-attdisc.gif "discriminação de atributos no Visualizador Naive Bayes")  
  
##### <a name="explore-attribute-discrimination"></a>Explorar distinção de atributo  
  
1.  Use os controles, **valor 1** e **valor 2**, para selecionar os resultados que você deseja comparar.  
  
     Por exemplo, nesse modelo havia alguns atributos interessantes no grupo de baixo rendimento, portanto, escolhemos o menor grupo de renda na primeira lista suspensa e escolhemos **todos os outros Estados** na segunda lista suspensa.  
  
     Os atributos são classificados por ordem de importância (calculada com base nos dados de treinamento). Consequentemente, a ocupação é o fator mais correlacionado com renda (para este grupo-alvo, pelo menos).  
  
     Para ver as figuras exatas, clique na barra colorida e exiba a **legenda de mineração**.  
  
2.  Observe que rendas mais baixas também estão correlacionadas com a região da Europa.  
  
     O modelo Naïve Bayes não oferece suporte à busca detalhada; no entanto, se você quiser verificar os casos associados a esse grupo de resultados, poderá usar uma consulta. Para obter informações sobre consultas sobre esse tipo de modelo, consulte [exemplos de consulta de modelo do Naive Bayes](data-mining/naive-bayes-model-query-examples.md).  
  
 [Voltar ao início](#BKMK_Tabs)  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisando modelos no Excel &#40;SQL Server suplementos de mineração de dados&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
