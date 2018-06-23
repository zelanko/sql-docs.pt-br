---
title: Procurando um modelo Naive Bayes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 36031bb080ff80c14a4f91bca102bd859df1f539
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006019"
---
# <a name="browsing-a-naive-bayes-model"></a>Procurando um modelo Naive Bayes
  Quando você abre um modelo de Naïve Bayes usando **procurar**, o modelo é exibido em um visualizador interativo com quatro painéis diferentes. Use o visualizador para explorar correlações e obter informações sobre o modelo e os dados subjacentes.  
  
-   [Rede de dependências](#bkmk_DepNet)  
  
-   [Perfis de atributo](#bkmk_AttProf)  
  
-   [Características do atributo](#bkmk_AttChar)  
  
-   [Distinção de atributo](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a> Explorar o modelo  
 A finalidade do visualizador é ajudar a explorar a interação entre os atributos de entrada e saída (entradas e variáveis dependentes) que foram descobertos pelo modelo Naïve Bayes da [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Se você quiser fazer experiências com o Visualizador de Naïve Bayes, use o [classificar assistente &#40;suplementos de mineração de dados para Excel&#41; ](classify-wizard-data-mining-add-ins-for-excel.md) assistente na faixa de opções mineração de dados, clique no **avançado** opção e alterar o algoritmo para usar o algoritmo Naïve Bayes  
  
 Para esses exemplos, é usada a fonte de dados na pasta de trabalho de exemplo e agrupamos a coluna **Renda anual**, em cinco grupos de renda, de **muito baixo** para **muito alta**. O modelo Naïve Bayes analisou os fatores correlacionadas com cada categoria de renda.  
  
###  <a name="bkmk_DepNet"></a> Rede de dependências  
 A primeira janela que você usará o **rede de dependência**. Ela mostra uma visão geral cujas entradas estão estreitamente correlacionadas ao resultado selecionado.  
  
 ![rede de dependências no visualizador Naive Bayes](media/dm13-nb.gif "rede de dependências no visualizador Naive Bayes")  
  
##### <a name="explore-the-dependency-network"></a>Explorar a rede de dependências  
  
1.  Primeiro, clique no resultado pretendido, **Renda anual**, que é representado como um nó no gráfico.  
  
     Os nós realçados em volta da variável pretendida são os que estão correlacionadas estatisticamente com esse resultado. Use a legenda na parte inferior do visualizador para entender a natureza da relação.  
  
2.  Clique no controle deslizante à esquerda do visualizador e arraste-o para baixo.  
  
     Esse controle filtra as variáveis independentes, com base nos pontos fortes das dependências. Quando você arrasta o controle deslizante para baixo, apenas os links mais importantes permanecem no gráfico.  
  
3.  Depois que você tiver filtrado o gráfico, clique no botão **Copiar exibição de gráfico**. Selecione uma planilha do Excel e pressione Ctrl+V.  
  
     Essa opção copia a exibição selecionada, inclusive filtros e realce.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a> Perfis de atributo  
 O **perfis de atributo** windows fornece uma indicação visual de como todas as outras variáveis estão relacionadas aos resultados individuais.  
  
##### <a name="explore-the-profiles"></a>Explorar os perfis  
  
1.  Para ocultar alguns valores para que você possa comparar resultados mais facilmente, clique no título da coluna e arraste-o para baixo de outra coluna.  
  
     ![atributo perfis no visualizador Naive Bayes](media/dm13-nb-attprof.gif "atributo perfis no visualizador Naive Bayes")  
  
2.  Clique em qualquer célula para exibir a distribuição de valores no **legenda de mineração**.  
  
     Como os atributos associados a resultados diferentes são exibidos visualmente, é fácil reconhecer correlações interessantes, por exemplo, como as rendas são distribuídas por região.  
  
3.  Para obter os dados subjacentes nessa exibição, clique em **copiar para Excel**. Uma tabela é gerada em uma nova planilha que mostra as correlações entre atributos individuais e resultados. Nessa tabela do Excel, você pode facilmente ocultar ou filtrar colunas.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a> Características do atributo  
 O **características do atributo** exibição é útil para a verificação detalhada de uma variável de resultado específico e os fatores de contribuição.  
  
 ![atributo características no visualizador Naive Bayes](media/dm13-nb-viewer.gif "atributo características no visualizador Naive Bayes")  
  
##### <a name="explore-the-attribute-characteristics"></a>Explorar as características do atributo  
  
1.  Clique em **valor** e selecione um item a partir de **valor**.  
  
     Quando você selecionar um resultado pretendido, o gráfico será atualizado para mostrar os fatores que estão mais fortemente associados ao resultado, classificados por importância.  
  
     Observe que, se você criar um modelo usando o [analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41; ](analyze-key-influencers-table-analysis-tools-for-excel.md) opção, você pode criar modelos que têm mais de um atributo previsível. No entanto, todos os outros assistentes nos suplementos de Mineração de Dados limitam a um atributo previsível.  
  
2.  Clique em **copiar para Excel** para criar uma tabela em uma nova planilha, listando as pontuações de todos os atributos relacionados ao resultado pretendido selecionado.  
  
 [Voltar ao início](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a> Distinção de atributo  
 O **distinção de atributo** exibir ajuda a comparar dois resultados ou um resultado versus todos os outros resultados.  
  
 ![atributo distinção no visualizador Naive Bayes](media/dm13-nb-attdisc.gif "atributo distinção no visualizador Naive Bayes")  
  
##### <a name="explore-attribute-discrimination"></a>Explorar distinção de atributo  
  
1.  Use os controles **valor 1** e **valor 2**, para selecionar os resultados que você deseja comparar.  
  
     Por exemplo, neste modelo havia alguns atributos interessantes no grupo de baixa renda, podemos escolher o grupo de renda mais baixo na primeira lista suspensa e escolher **todos os outros estados** na segunda lista suspensa.  
  
     Os atributos são classificados por ordem de importância (calculada com base nos dados de treinamento). Consequentemente, a ocupação é o fator mais correlacionado com renda (para este grupo-alvo, pelo menos).  
  
     Para ver os valores exatos, clique a barra colorida e exiba o **legenda de mineração**.  
  
2.  Observe que rendas mais baixas também estão correlacionadas com a região da Europa.  
  
     O modelo Naïve Bayes não oferece suporte à busca detalhada; no entanto, se você quiser verificar os casos associados a esse grupo de resultados, poderá usar uma consulta. Para obter informações sobre esse tipo de modelo, consulte [Naive Bayes Model Query Examples](data-mining/naive-bayes-model-query-examples.md).  
  
 [Voltar ao início](#BKMK_Tabs)  
  
## <a name="see-also"></a>Consulte também  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  