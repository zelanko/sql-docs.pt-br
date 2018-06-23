---
title: Explorando o modelo de previsão (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0a00f409-050f-4b92-9763-ba31a6aa3052
caps.latest.revision: 52
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6f6cffb56dd4ef4a9df6618ce126e2b3d0340640
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313034"
---
# <a name="exploring-the-forecasting-model-intermediate-data-mining-tutorial"></a>Explorando o modelo de previsão (tutorial de mineração de dados intermediário)
  Agora que você criou o modelo de mineração de previsão, você pode explorar os resultados usando o **Visualizador do modelo de mineração** guia do Designer de mineração de dados. O [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizador Time Series contém duas guias: **gráficos** e **modelo**.  
  
 Além disso, você pode usar o Visualizador de Árvore de Conteúdo Genérica da Microsoft com todos os modelos. Cada exibição apresenta uma imagem ligeiramente das informações no modelo de série temporal.  
  
-   [Guia gráficos](#bkmk_Charts)  
  
-   [Guia modelo](#bkmk_Model)  
  
-   [Visualizador de conteúdo genérica da Microsoft](#bkmk_Content)  
  
##  <a name="bkmk_Charts"></a> Guia gráficos  
 O **gráficos** guia o [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizador Time Series mostra graficamente cada uma das séries, incluindo dados históricos e previsões. Cada linha do gráfico de série temporal representa uma combinação única de produto, região e atributo previsível.  
  
 A legenda à direita do visualizador relaciona a série temporal disponível, com base nas seleções na lista suspensa. É possível marcar e desmarcar as caixas de seleção na legenda para controlar a série temporal exibida no gráfico.  
  
 Também é possível alterar as opções de exibição, como as cores usadas em cada série temporal, ou se os valores são exibidos em pontos do gráfico.  
  
#### <a name="to-select-a-time-series"></a>Para selecionar uma série temporal  
  
1.  Clique no **gráficos** guia o **Visualizador do modelo de mineração** guia, se não estiver visível.  
  
2.  Clique na lista suspensa à direita da exibição do gráfico e marque todas as caixas de seleção: [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Agora o gráfico deve conter 24 linhas de séries diferentes.  
  
3.  Desmarque as caixas de seleção à direita do gráfico para ocultar temporariamente as linhas de todas as séries que se baseiem em Valor.  
  
     Agora, desmarque as caixas de seleção relacionadas às bicicletas R750 e R250.  
  
     Agora o gráfico contém apenas as seis linhas de série para que seja possível comparar mais facilmente as tendências para as bicicletas M200 e T1000.  
  
    -   **M200 Europe: Quantity**  
  
    -   **M200 América do Norte: quantidade**  
  
    -   **M200 Pacífico: quantidade**  
  
    -   **T1000 Europe: Quantity**  
  
    -   **T1000 América do Norte: quantidade**  
  
    -   **T1000 Pacífico: quantidade**  
  
 ![Séries que preveem a quantidade M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "séries que preveem a quantidade M200 e T1000")  
  
 O gráfico que é exibido neste visualizador inclui dados históricos e previstos. Os dados previstos aparecem sombreados para diferenciá-los dos dados históricos. Para facilitar a comparação de séries diferentes, também é possível alterar as cores associadas a cada linha no gráfico. Para obter mais informações, consulte [Alterar as cores usadas no Visualizador de mineração de dados](../../2014/analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md).  
  
 As linhas de tendência mostram que o total de vendas para todas as regiões normalmente cresce, com pico a cada 12 meses, em dezembro. No gráfico, você também pode ver que os dados para a bicicleta T1000 começam muito depois dos dados para a outra série de produto. Isso é porque é um produto mais novo, mas como esta série é baseada em muito menos dados, as previsões podem não ser tão precisas.  
  
 Por padrão, cinco etapas de previsão são mostradas para cada série temporal, exibidas como linhas pontilhadas. É possível alterar esse valor para exibir mais ou menos previsões. Também é possível exibir graficamente o desvio padrão para as previsões adicionando-se barras de erro ao gráfico.  
  
#### <a name="to-change-prediction-and-display-options-in-the-chart-view"></a>Para alterar as opções de previsão e exibição na exibição do Gráfico  
  
1.  Tente alterar o valor de **etapas de previsão** gradativamente, aumentando de **5** para **10**e, em seguida, de volta para **6**.  
  
     Quando os dados históricos apresentam grandes flutuações, as flutuações tendem a ser repetidas ou até mesmo ampliadas conforme você aumenta o número de previsões. Neste momento, você precisa pesquisar para entender a causa do grande aumento nos dados históricos e depois decidir se aceita os resultados, se procura algum tipo de correção nos dados de origem ou se aplica algum tipo de atenuação no modelo.  
  
2.  Selecione o **Mostrar desvios** caixa de seleção.  
  
     Esta opção exibe o erro estimado para cada valor previsto.  
  
3.  Observe a escala do eixo x. As alterações dos dados históricos e previstos são sempre expressas como porcentagem, mas os valores reais são ajustados automaticamente para acomodar todos os valores no gráfico. Portanto, é preciso ter cuidado ao comparar modelos para não confiar somente no visual. Para obter exatamente valor, ou o aumento percentual e o valor de previsões, pare o mouse sobre a linha pontilhada ou linhas sólidas ou clique nas linhas para exibir os valores no **legenda de mineração**.  
  
     **Dica**: se o **legenda de mineração** não estiver visível, alterne para o **modelo** exibir, qualquer nó e selecione **Mostrar legenda**.  
  
 Observando essas tendências, você ficou preocupado com a falta de dados em algumas séries ou quer saber se poderá obter previsões mais confiáveis calculando a média de vendas por modelo, ou talvez por região. Você explorará esse método posteriormente em uma lição neste tutorial.  
  
 [Voltar ao início](#bkmk_Charts)  
  
##  <a name="bkmk_Model"></a> Guia modelo  
 O **modelo** guia o [!INCLUDE[msCoName](../includes/msconame-md.md)] visualizador MTS no Designer de mineração de dados permite que você exiba o modelo de previsão na forma de um gráfico de árvore.  
  
 Primeiramente, observe que, como seus dados descrevem duas medidas diferentes (Valor e Quantidade) para as vendas de várias linhas de produtos (T1000 etc.) em três regiões diferentes (Europa, América do Norte e Pacífico), o modelo que você criou contém, na verdade, 24 árvores diferentes, cada uma representando um modelo dos padrões de vendas de uma combinação diferente de região, produto e atributo previsível.  
  
 Você pode escolher qual combinação de linha de produto, região e métrica de vendas que você deseja exibir selecionando uma série do **árvore** lista suspensa de **modelo** guia.  
  
 Então, o que você pode perceber vendo o modelo como uma árvore? Como um exemplo, vamos comparar dois modelos, um que tem vários níveis na árvore e outro que tem um único nó.  
  
-   Quando um gráfico de árvore contém um único nó, significa que a tendência encontrada no modelo fica mais homogênea com o passar do tempo. Você pode usar esse único nó, denominado **todos os**, para exibir a fórmula que descreve a relação entre as variáveis de entrada e o resultado.  
  
-   Quando um gráfico de árvore de uma série temporal tem várias ramificações, significa que a série temporal detectada é muito complexa para ser representada como uma única equação. Em vez disso, o gráfico de árvore pode conter várias ramificações, cada ramificação rotulada com as condições que causaram a árvore *dividir*. Quando a árvore é dividida, cada ramificação representa um segmento diferente de tempo, dentro do qual a tendência pode ser descrita como uma única equação.  
  
     Por exemplo, se você examinar o gráfico e perceber um salto súbito no volume de vendas iniciando em determinado momento em setembro e continuando até um feriado de fim de ano, você pode alternar para o **modelo** modo de exibição para ver a data exata em que a tendência mudou. As ramificações na árvore que representam "antes de setembro" e "depois de setembro" conteriam fórmulas diferentes: uma fórmula que descreve matematicamente as tendências de vendas até a divisão e outra fórmula que descreve as tendências de vendas para setembro até o feriado de fim de ano.  
  
#### <a name="to-explore-the-decision-tree-for-a-time-series-model"></a>Para explorar a árvore de decisão para um modelo de série temporal  
  
1.  No **árvore** lista o **modelo** guia do visualizador, selecione o **T1000 Europe: quantidade** série.  
  
     Clique no nó denominado **todos os**.  
  
     Para uma **todos os** nó, a dica de ferramenta que aparece inclui informações como o número de casos em toda a série e equações de série temporal derivadas da análise dos dados.  
  
2.  Se o **legenda de mineração** não estiver visível, clique com botão direito no nó e selecione **Mostrar legenda**.  
  
     O **legenda de mineração** fornece basicamente as mesmas informações que está na dica de ferramenta. Se alguma de suas variáveis independentes estiver oculta, você também verá um histograma que mostra a distribuição de variáveis no nó.  
  
3.  Agora selecione uma série temporal diferente para exibir. Usando o **árvore** lista o **modelo** guia do visualizador, selecione o **M200 América do Norte: quantidade** série.  
  
     Agora, o gráfico de árvore contém um **todos os** nó e dois nós filho. Observando os títulos dos nós filho, você pode saber em que ponto a linha de tendência mudou.  
  
     Para cada nó filho, a descrição no **legenda de mineração** também inclui a contagem de casos em cada ramificação da árvore.  
  
 A lista a seguir descreve alguns recursos adicionais do visualizador de árvore:  
  
-   Você pode alterar a variável que é representada no gráfico usando o **em segundo plano** controle. Por padrão, nós mais escuros contêm mais casos, porque o valor de **em segundo plano** é definido como **população**. Para ver somente quantos casos há em um nó, coloque o mouse sobre um nó e exiba a dica de ferramenta que aparece, ou clique no nó e exibir os números de **legenda de nó** janela.  
  
-   A fórmula de regressão para o nó também pode ser exibida na Dica de Ferramenta, ou clicando no nó. Se você tiver criado um modelo misto, poderá ver duas fórmulas, uma para ARTXP (nos nós folha) e um para ARIMA (no nó raiz da árvore).  
  
-   Os pequenos losangos são usados nos nós que representam números contínuos. O intervalo dos atributos é mostrado na barra em que se encontra o losango. O losango fica centralizado na posição mediana do nó, e sua largura representa a variação do atributo naquele nó.  
  
 [Voltar ao início](#bkmk_Charts)  
  
##  <a name="bkmk_Content"></a> (Opcional) Visualizador de árvore de conteúdo genérica  
 Além do visualizador personalizado para a série temporal, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece o **Visualizador de árvore de conteúdo MicrosoftGeneric** para uso com todos os modelos de mineração de dados. Este visualizador fornece algumas vantagens:  
  
-   **Visualizador MTS**: este modo de exibição combina os resultados dos dois algoritmos. Embora você possa exibir cada série separadamente, não é possível determinar como os resultados de cada algoritmo são combinados. Além disso, nessa exibição, as Dicas de Ferramenta e a Legenda de Mineração mostram somente as estatísticas mais importantes.  
  
-   **Visualizador de árvore de conteúdo genérica**: permite que você navegue e exibir todas as séries de dados que foram usadas no modelo ao mesmo tempo e se você tiver criado um misto de modelo, ambos os ARIMA e árvores ARTXP são exibidos no mesmo gráfico.  
  
     Você pode usar esse visualizador para obter todas as estatísticas de ambos os algoritmos, bem como as distribuições dos valores.  
  
     Recomendado para usuários especialistas em mineração de dados que desejam saber mais sobre as análises ARIMA e ARTXP.  
  
#### <a name="to-view-details-for-a-particular-data-series-in-the-generic-content-viewer"></a>Para exibir detalhes de uma determinada série de dados no visualizador de conteúdo genérico  
  
1.  No **Visualizador do modelo de mineração** guia, selecione **Microsoft Visualizador de árvore de conteúdo genérica** do **visualizador** lista suspensa.  
  
2.  No **legenda de nó** painel, clique com o primeiro nó (All).  
  
3.  No **detalhes do nó** painel, exiba o valor de ATTRIBUTE_NAME.  
  
     Esse valor mostra qual série, ou combinação de produto e região, está contida nesse nó. No exemplo do AdventureWorks, o nó superior pertence à série M200 Europe.  
  
4.  No **legenda de nó** painel, localize o primeiro nó que tem nós filhos.  
  
     Se um nó de série tiver filhos, a exibição de árvore que aparece no **modelo** guia do visualizador MTS também terá uma estrutura de ramificação.  
  
5.  Expanda o nó e clique em um dos nós filho.  
  
     A coluna NODE_DESCRIPTION do esquema contém a condição que causou a divisão da árvore.  
  
6.  No **legenda de nó** painel, clique no nó ARIMA superior e expanda o nó até que todos os nós filho são visíveis.  
  
7.  No **detalhes do nó** painel, exiba o valor de ATTRIBUTE_NAME.  
  
     Esse valor informa qual série temporal está contida nesse nó. O nó superior na seção ARIMA corresponde ao nó superior na seção (Tudo). No exemplo do AdventureWorks, esse nó contém a análise ARIMA da série M200 Europe.  
  
 Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de série temporal &#40;Analysis Services – Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md).  
  
 [Voltar ao início](#bkmk_Charts)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criando previsões de série temporal &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de consulta de modelo de série temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Referência técnica do algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  