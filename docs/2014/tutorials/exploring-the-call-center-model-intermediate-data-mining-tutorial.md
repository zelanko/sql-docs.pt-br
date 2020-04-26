---
title: Explorando o modelo do Call Center (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9095212c-9068-4dd8-85ce-17a467adeabb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6aa4074aa04af86e478b57b1870fd0dd855bea8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63315076"
---
# <a name="exploring-the-call-center-model-intermediate-data-mining-tutorial"></a>Explorando o modelo de call center (Tutorial de mineração de dados intermediário)
  Agora que você criou o modelo exploratório, poderá usá-lo para saber mais sobre os dados utilizando as ferramentas a seguir fornecidas no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   [Visualizador de rede neural da Microsoft](#bkmk_NNviewer) **:** este visualizador está disponível na guia **Visualizador do modelo de mineração** do designer de mineração de dados e foi projetado para ajudá-lo a experimentar as interações nos dados.  
  
-   [Visualizador de árvore de conteúdo genérica da Microsoft](#bkmk_genviewer) **:** este visualizador padrão fornece detalhes detalhados sobre os padrões e estatísticas descobertos pelo algoritmo quando ele gerou o modelo.  
  
##  <a name="microsoft-neural-network-viewer"></a><a name="bkmk_NNviewer"></a>Visualizador de rede neural da Microsoft  
 O visualizador tem três painéis – **entrada**, **saída**e **variáveis**.  
  
 Usando o painel **saída** , você pode selecionar valores diferentes para o atributo previsível ou para a variável dependente. Se o modelo contiver vários atributos previsíveis, você poderá selecionar o atributo na lista **atributo de saída** .  
  
 O painel **variáveis** compara os dois resultados que você escolheu em termos de atributos ou variáveis contribuintes. As barras coloridas representam visualmente com que intensidade a variável afeta os resultados de destino. Você também pode exibir pontuações de comparação de precisão para as variáveis. Uma pontuação de comparação de precisão é calculada de modo diferente de acordo com o tipo de modelo de mineração utilizado, mas geralmente informa o aperfeiçoamento no modelo durante o uso desse atributo para previsão.  
  
 O painel **entrada** permite adicionar influenciadores ao modelo para experimentar vários cenários hipotéticos.  
  
### <a name="using-the-output-pane"></a>Usando o painel Saída  
 Neste modelo inicial, você está interessado em verificar como vários fatores afetam a classificação do serviço. Para fazer isso, você pode selecionar a classificação de serviço na lista de atributos de saída e comparar diferentes níveis de serviço selecionando intervalos nas listas suspensas para **valor 1** e **valor 2**.  
  
##### <a name="to-compare-lowest-and-highest-service-grades"></a>Para comparar as classificações de serviço mais baixa e mais alta  
  
1.  Para o **valor 1**, selecione o intervalo com os valores mais baixos. Por exemplo, o intervalo 0-0-0.7 representa as taxas de abandono mais baixas e, portanto, o melhor nível de serviço.  
  
    > [!NOTE]  
    >  Os valores exatos nesse intervalo podem variar de acordo com a configuração do modelo.  
  
2.  Para **valor 2**, selecione o intervalo com os valores mais altos. Por exemplo, o intervalo com o valor >= 0,12 representa as taxas de abandono mais altas e, portanto, a pior taxa de serviço. Em outras palavras, 12% dos clientes que telefonaram durante esse turno desligaram antes de falar com um atendente.  
  
     O conteúdo do painel **variáveis** é atualizado para comparar os atributos que contribuem com os valores de resultado. Assim, a coluna esquerda mostra os atributos associados à melhor classificação de serviço, e a coluna direita mostra o atributo associado à pior classificação do serviço.  
  
### <a name="using-the-variables-pane"></a>Usando o painel Variáveis  
 Nesse modelo, parece que `Average Time Per Issue` se trata de um fator importante. Essa variável indica o tempo médio necessário para que uma chamada seja atendida, independentemente do tipo de chamada.  
  
##### <a name="to-view-and-copy-probability-and-lift-scores-for-an-attribute"></a>Para exibir e copiar a probabilidade e as pontuações de comparação de precisão para um atributo  
  
1.  No painel **variáveis** , pause o mouse sobre a barra colorida na primeira linha.  
  
     Esta barra colorida mostra a você como `Average Time Per Issue` contribui bastante para a classificação de serviço. A dica de ferramenta mostra uma pontuação geral, as probabilidades e as pontuações de comparação de precisão para cada combinação de uma variável e um resultado de destino.  
  
2.  No painel **variáveis** , clique com o botão direito do mouse em qualquer barra colorida e selecione **copiar**.  
  
3.  Em uma planilha do Excel, clique com o botão direito do mouse em qualquer célula e selecione **colar**.  
  
     O relatório é colado como uma tabela HTML e mostra apenas as pontuações para cada barra.  
  
4.  Em uma planilha do Excel diferente, clique com o botão direito do mouse em qualquer célula e selecione **colar especial**.  
  
     O relatório é colado como formato de texto e inclui as estatísticas relacionadas descritas na próxima seção.  
  
### <a name="using-the-input-pane"></a>Usando o painel Entrada  
 Vamos supor que você esteja interessado em examinar o efeito de um determinado fator, como o turno ou o número de operadores. Você pode selecionar uma variável específica usando o painel de **entrada** e o painel **variáveis** é atualizado automaticamente para comparar os dois grupos selecionados anteriormente, considerando a variável especificada.  
  
##### <a name="to-review-the-effect-on-service-grade-by-changing-input-attributes"></a>Para examinar o efeito na classificação de serviço alterando os atributos de entrada  
  
1.  No painel de **entrada** , para **atributo**, selecione Shift.  
  
2.  Para **valor**, selecione **am**.  
  
     O painel **variáveis** **é atualizado**para mostrar o impacto no modelo quando a mudança é. Todas as outras seleções permanecem as mesmas-você ainda está comparando as notas de serviço mais baixas e mais altas.  
  
3.  Para **valor**, selecione **PM1**.  
  
     O painel **variáveis** é atualizado para mostrar o impacto no modelo quando a mudança é alterada.  
  
4.  No painel de **entrada** , clique na próxima linha em branco em **atributo**e selecione chamadas. Para **valor**, selecione o intervalo que indica o maior número de chamadas.  
  
     Uma nova condição de entrada é adicionada à lista. O painel **variáveis** é atualizado para mostrar o impacto no modelo para uma mudança específica quando o volume de chamada é mais alto.  
  
5.  Continue para alterar os valores para Turno e Chamadas de modo a encontrar correlações interessantes entre o turno, o volume de chamadas e a classificação do serviço.  
  
    > [!NOTE]  
    >  Para limpar o painel de **entrada** para que você possa usar atributos diferentes, clique em **Atualizar conteúdo do visualizador**.  
  
### <a name="interpreting-the-statistics-provided-in-the-viewer"></a>Interpretando as estatísticas fornecidas no visualizador  
 Tempos de espera mais longos constituem um fator importante para uma taxa de abandono alta, indicando uma classificação de serviço mais fraca. Essa pode ser considerada uma conclusão óbvia; no entanto, o modelo de mineração fornece mais alguns dados estatísticos adicionais para ajudar a interpretar essas tendências.  
  
-   **Score**: valor que indica a importância geral dessa variável para discriminar entre os resultados. Quanto mais alta for a pontuação, maior o efeito da variável no resultado.  
  
-   **Probabilidade do valor 1**: porcentagem que representa a probabilidade desse valor para esse resultado.  
  
-   **Probabilidade de valor 2**: porcentagem que representa a probabilidade desse valor para esse resultado.  
  
-   **Levante para o valor 1** e **levante para o valor 2**: pontuações que representam o impacto de usar essa variável específica para prever os resultados do valor 1 e do valor 2. Quanto mais alta for a pontuação, melhor será a variável para prever os resultados.  
  
 A tabela a seguir contém alguns valores de exemplo para os influenciadores principais. Por exemplo, a **probabilidade de valor 1 é de** 60,6% e a **probabilidade de valor 2** é 8,30%, o que significa que, quando o tempo médio por problema estava no intervalo de 44-70 minutos, 60,6% dos casos estava na mudança com as mais altas notas de serviço (valor 1) e 8,30% dos casos que estavam na mudança com as piores notas de serviço (valor 2).  
  
 Com base nessas informações, é possível estabelecer algumas conclusões. O menor tempo de resposta para chamada (o intervalo de 44-70) influencia fortemente a melhor classificação do serviço (o intervalo 0,00-0,07). A pontuação (92,35) informa que essa variável é muito importante.  
  
 Entretanto, à medida que você examina a lista de fatores contribuintes, percebe alguns outros fatores  Por exemplo, o turno parece influenciar o serviço, mas as pontuações de comparação de precisão e as probabilidades relativas indicam que o turno não é um fator preponderante.  
  
|Atributo|Valor|Favorece \< 0, 7|Favorece >= 0,12|  
|---------------|-----------|--------------------|----------------------|  
|Tempo médio por emissão|89, 87-120, 0||Pontuação: 100<br /><br /> Probabilidade de value1:4,45%<br /><br /> Probabilidade de value2:51,94%<br /><br /> Levante para value1:0,19<br /><br /> Levante para value2:1,94|  
|Tempo médio por emissão|44, 0-70,597|Pontuação: 92,35<br /><br /> Probabilidade do Valor 1: 60,06 %<br /><br /> Probabilidade do Valor 2: 8,30 %<br /><br /> Comparação de Precisão para o Valor 1: 2,61<br /><br /> Comparação de Precisão para o Valor 2: 0,31||  
  
 [Voltar ao início](#bkmk_NNviewer)  
  
##  <a name="microsoft-generic-content-tree-viewer"></a><a name="bkmk_genviewer"></a>Visualizador de árvore de conteúdo genérica da Microsoft  
 Este visualizador pode ser usado para exibir informações ainda mais detalhadas criadas pelo algoritmo durante o processamento do modelo. O **Visualizador de árvore de conteúdo MicrosoftGeneric** representa o modelo de mineração como uma série de nós, em que cada nó representa conhecimento aprendido sobre os dados de treinamento. Esse visualizador pode ser usado com todos os modelos, mas o conteúdo dos nós é diferente de acordo com o tipo de modelo.  
  
 Para modelos de rede neural ou de regressão logística, talvez você ache o `marginal statistics node` particularmente útil. Esse nó contém estatísticas derivadas sobre a distribuição de valores nos dados. Essas informações poderão ser úteis se você quiser obter um resumo dos dados sem escrever muitas consultas T-SQL. O gráfico de valores de compartimento no tópico anterior foi derivado do nó de estatísticas marginais.  
  
#### <a name="to-obtain-a-summary-of-data-values-from-the-mining-model"></a>Para obter um resumo dos valores de dados do modelo de mineração  
  
1.  No designer de mineração de dados, na guia **Visualizador do modelo** de \<mineração, selecione nome do modelo de mineração>.  
  
2.  Na lista **Visualizador** , selecione **Visualizador de árvore de conteúdo genérica da Microsoft**.  
  
     A exibição do modelo de mineração é atualizada para mostrar uma hierarquia de nós no painel esquerdo e uma tabela HTML no painel direito.  
  
3.  No painel **legenda do nó** , clique no nó que tem o nome 10000000000000000.  
  
     O nó na extremidade superior em qualquer modelo sempre é o nó raiz do modelo. Em um modelo de rede neural ou de regressão logística, o nó imediatamente sob esse é o nó de estatísticas marginais.  
  
4.  No painel **detalhes do nó** , role para baixo até encontrar a linha NODE_DISTRIBUTION.  
  
5.  Role para baixo pela tabela NODE_DISTRIBUTION para exibir a distribuição de valores conforme calculados pelo algoritmo de rede neural.  
  
 Para usar esses dados em um relatório, selecione e copie as informações para linhas específicas ou use a consulta DMX a seguir para extrair todo o conteúdo do nó.  
  
```  
SELECT *   
FROM [Call Center EQ4].CONTENT  
WHERE NODE_NAME = '10000000000000000'  
```  
  
 Também é possível usar a hierarquia de nós e os detalhes na tabela NODE_DISTRIBUTION para desviar caminhos individuais na rede neural e exibir estatísticas da camada oculta. Para obter mais informações, consulte [exemplos de consulta de modelo de rede neural](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 [Voltar ao início](#bkmk_NNviewer)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Adicionando um modelo de regressão logística à estrutura do Call Center &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services&#41;de mineração de dados](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelo de rede neural](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Referência técnica do algoritmo rede neural da Microsoft](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Alterar a diferenciação de uma coluna em um modelo de mineração](../../2014/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)  
  
  
