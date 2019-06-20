---
title: Explorando o modelo de Call Center (Tutorial de mineração de dados intermediário) | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63315076"
---
# <a name="exploring-the-call-center-model-intermediate-data-mining-tutorial"></a>Explorando o modelo de call center (Tutorial de mineração de dados intermediário)
  Agora que você criou o modelo exploratório, poderá usá-lo para saber mais sobre os dados utilizando as ferramentas a seguir fornecidas no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   [Visualizador de rede Neural da Microsoft](#bkmk_NNviewer) **:** Este visualizador está disponível na **Visualizador do modelo de mineração** guia do Designer de mineração de dados e foi projetado para ajudá-lo a testar as interações nos dados.  
  
-   [Microsoft Generic Content Tree Viewer](#bkmk_genviewer) **:** Este visualizador padrão fornece detalhes sobre os padrões e estatísticas identificadas pelo algoritmo durante a geração do modelo.  
  
##  <a name="bkmk_NNviewer"></a> Visualizador de rede Neural da Microsoft  
 O visualizador tem três painéis - **entrada**, **saída**, e **variáveis**.  
  
 Usando o **saída** painel, você pode selecionar valores diferentes para o atributo previsível ou variável dependente. Se seu modelo contiver vários atributos previsíveis, você pode selecionar o atributo do **atributo de saída** lista.  
  
 O **variáveis** painel compara os dois resultados escolhidos em termos de atributos de colaboração ou variáveis. As barras coloridas representam visualmente com que intensidade a variável afeta os resultados de destino. Você também pode exibir pontuações de comparação de precisão para as variáveis. Uma pontuação de comparação de precisão é calculada de modo diferente de acordo com o tipo de modelo de mineração utilizado, mas geralmente informa o aperfeiçoamento no modelo durante o uso desse atributo para previsão.  
  
 O **entrada** painel permite adicionar influenciadores ao modelo para testar vários cenários hipotéticos.  
  
### <a name="using-the-output-pane"></a>Usando o painel Saída  
 Neste modelo inicial, você está interessado em verificar como vários fatores afetam a classificação do serviço. Para fazer isso, você pode selecionar o nível de serviço na lista de atributos de saída e, em seguida, compare diferentes níveis de serviço selecionando intervalos nas listas suspensas para **valor 1** e **valor 2**.  
  
##### <a name="to-compare-lowest-and-highest-service-grades"></a>Para comparar as classificações de serviço mais baixa e mais alta  
  
1.  Para **valor 1**, selecione o intervalo com os valores mais baixos. Por exemplo, o intervalo 0-0-0.7 representa as taxas de abandono mais baixas e, portanto, o melhor nível de serviço.  
  
    > [!NOTE]  
    >  Os valores exatos nesse intervalo podem variar de acordo com a configuração do modelo.  
  
2.  Para **valor 2**, selecione o intervalo com os valores mais altos. Por exemplo, o intervalo com o valor > = gt;=0.12 representa as taxas de abandono mais altas e, portanto, a pior classificação de serviço. Em outras palavras, 12% dos clientes que telefonaram durante esse turno desligaram antes de falar com um atendente.  
  
     O conteúdo a **variáveis** painel são atualizados para comparar os atributos que contribuem para os valores de resultado. Assim, a coluna esquerda mostra os atributos associados à melhor classificação de serviço, e a coluna direita mostra o atributo associado à pior classificação do serviço.  
  
### <a name="using-the-variables-pane"></a>Usando o painel Variáveis  
 Nesse modelo, parece que `Average Time Per Issue` é um fator importante. Essa variável indica o tempo médio necessário para que uma chamada seja atendida, independentemente do tipo de chamada.  
  
##### <a name="to-view-and-copy-probability-and-lift-scores-for-an-attribute"></a>Para exibir e copiar a probabilidade e as pontuações de comparação de precisão para um atributo  
  
1.  No **variáveis** painel, coloque o mouse sobre a barra colorida na primeira linha.  
  
     Essa barra colorida mostra com que intensidade `Average Time Per Issue` colabora para o nível de serviço. A dica de ferramenta mostra uma pontuação geral, as probabilidades e as pontuações de comparação de precisão para cada combinação de uma variável e um resultado de destino.  
  
2.  No **variáveis** painel, clique com botão direito qualquer barra colorida e selecione **cópia**.  
  
3.  Em uma planilha do Excel, clique em qualquer célula e selecione **colar**.  
  
     O relatório é colado como uma tabela HTML e mostra apenas as pontuações para cada barra.  
  
4.  Em outra planilha do Excel, clique em qualquer célula e selecione **Colar especial**.  
  
     O relatório é colado como formato de texto e inclui as estatísticas relacionadas descritas na próxima seção.  
  
### <a name="using-the-input-pane"></a>Usando o painel Entrada  
 Vamos supor que você esteja interessado em examinar o efeito de um determinado fator, como o turno ou o número de operadores. Você pode selecionar uma determinada variável usando o **entrada** painel e o **variáveis** painel é atualizado automaticamente para comparar os dois anteriormente grupos selecionados, dado que a variável especificada.  
  
##### <a name="to-review-the-effect-on-service-grade-by-changing-input-attributes"></a>Para examinar o efeito na classificação de serviço alterando os atributos de entrada  
  
1.  No **entrada** painel, para **atributo**, selecione turno.  
  
2.  Para **valor**, selecione **AM**.  
  
     O **variáveis** atualizações de painel para mostrar o impacto no modelo quando o turno é **AM**. Todas as outras seleções permanecem os mesmos, você ainda está comparando os níveis de serviço menor e maior.  
  
3.  Para **valor**, selecione **PM1**.  
  
     O **variáveis** painel é atualizado para mostrar o impacto no modelo quando o turno é alterado.  
  
4.  No **entrada** painel, clique na próxima linha em branco sob **atributo**e selecione chamadas. Para **valor**, selecione o intervalo que indica o maior número de chamadas.  
  
     Uma nova condição de entrada é adicionada à lista. O **variáveis** painel é atualizado para mostrar o impacto no modelo de um determinado turno quando o volume de chamada é mais alto.  
  
5.  Continue para alterar os valores para Turno e Chamadas de modo a encontrar correlações interessantes entre o turno, o volume de chamadas e a classificação do serviço.  
  
    > [!NOTE]  
    >  Para limpar os **entrada** painel para que você possa usar atributos diferentes, clique em **atualizar conteúdo do visualizador**.  
  
### <a name="interpreting-the-statistics-provided-in-the-viewer"></a>Interpretando as estatísticas fornecidas no visualizador  
 Tempos de espera mais longos constituem um fator importante para uma taxa de abandono alta, indicando uma classificação de serviço mais fraca. Essa pode ser considerada uma conclusão óbvia; no entanto, o modelo de mineração fornece mais alguns dados estatísticos adicionais para ajudar a interpretar essas tendências.  
  
-   **Pontuação**: Valor que indica a importância geral dessa variável para Discriminar entre os resultados. Quanto mais alta for a pontuação, maior o efeito da variável no resultado.  
  
-   **Probabilidade do valor 1**: Porcentagem que representa a probabilidade desse valor para esse resultado.  
  
-   **Probabilidade do valor 2**: Porcentagem que representa a probabilidade desse valor para esse resultado.  
  
-   **Comparação de precisão para o valor 1** e **comparação de precisão para o valor 2**: Pontuações que representam o impacto de usar essa variável em particular para prever os resultados do valor 1 e 2 do valor. Quanto mais alta for a pontuação, melhor será a variável para prever os resultados.  
  
 A tabela a seguir contém alguns valores de exemplo para os influenciadores principais. Por exemplo, o **probabilidade do valor 1** é 60,6% e **probabilidade do valor 2** é 8,30%, que significa que, quando o tempo médio por emissão estava no intervalo de 44-70 minutos, 60,6% dos casos ocorreram no turno com o níveis de serviço mais altas (valor 1) e 8,30% dos casos ocorreram no turno com as piores classificações de serviço (valor 2).  
  
 Com base nessas informações, é possível estabelecer algumas conclusões. O menor tempo de resposta para chamada (o intervalo de 44-70) influencia fortemente a melhor classificação do serviço (o intervalo 0,00-0,07). A pontuação (92,35) informa que essa variável é muito importante.  
  
 Entretanto, à medida que você examina a lista de fatores contribuintes, percebe alguns outros fatores Por exemplo, o turno parece influenciar o serviço, mas as pontuações de comparação de precisão e as probabilidades relativas indicam que o turno não é um fator preponderante.  
  
|attribute|Valor|Favorece \< 0,07|Favorece > = 0,12|  
|---------------|-----------|--------------------|----------------------|  
|Tempo médio por emissão|89.087 - 120.000||Pontuação:  100<br /><br /> Probabilidade de valor1: 4.45 %<br /><br /> Probabilidade de Value2: 51.94 %<br /><br /> Comparação de precisão de valor1: 0.19<br /><br /> Comparação de precisão para Value2: 1.94|  
|Tempo médio por emissão|44.000 - 70.597|Pontuação: 92.35<br /><br /> Probabilidade de valor1: 60.06 %<br /><br /> Probabilidade de Value2: 8.30 %<br /><br /> Comparação de precisão de valor1: 2.61<br /><br /> Comparação de precisão para Value2: 0.31||  
  
 [Voltar ao Início](#bkmk_NNviewer)  
  
##  <a name="bkmk_genviewer"></a> Visualizador de árvore de conteúdo genérica da Microsoft  
 Este visualizador pode ser usado para exibir informações ainda mais detalhadas criadas pelo algoritmo durante o processamento do modelo. O **Visualizador de árvore de conteúdo MicrosoftGeneric** representa o modelo de mineração como uma série de nós, no qual cada nó representa conhecimento adquirido sobre os dados de treinamento. Esse visualizador pode ser usado com todos os modelos, mas o conteúdo dos nós é diferente de acordo com o tipo de modelo.  
  
 Para modelos de rede neural ou de regressão logística, talvez você ache o `marginal statistics node` particularmente útil. Esse nó contém estatísticas derivadas sobre a distribuição de valores nos dados. Essas informações poderão ser úteis se você quiser obter um resumo dos dados sem escrever muitas consultas T-SQL. O gráfico de valores de compartimento no tópico anterior foi derivado do nó de estatísticas marginais.  
  
#### <a name="to-obtain-a-summary-of-data-values-from-the-mining-model"></a>Para obter um resumo dos valores de dados do modelo de mineração  
  
1.  No Designer de mineração de dados, nos **Visualizador do modelo de mineração** guia, selecione \<nome do modelo de mineração >.  
  
2.  Dos **Viewer** lista, selecione **Microsoft genérico conteúdo Visualizador de árvore**.  
  
     A exibição do modelo de mineração é atualizada para mostrar uma hierarquia de nós no painel esquerdo e uma tabela HTML no painel direito.  
  
3.  No **legenda de nó** painel, clique no nó que tem o nome 10000000000000000.  
  
     O nó na extremidade superior em qualquer modelo sempre é o nó raiz do modelo. Em um modelo de rede neural ou de regressão logística, o nó imediatamente sob esse é o nó de estatísticas marginais.  
  
4.  No **detalhes do nó** painel, role para baixo até encontrar a linha NODE_DISTRIBUTION.  
  
5.  Role para baixo pela tabela NODE_DISTRIBUTION para exibir a distribuição de valores conforme calculados pelo algoritmo de rede neural.  
  
 Para usar esses dados em um relatório, selecione e copie as informações para linhas específicas ou use a consulta DMX a seguir para extrair todo o conteúdo do nó.  
  
```  
SELECT *   
FROM [Call Center EQ4].CONTENT  
WHERE NODE_NAME = '10000000000000000'  
```  
  
 Também é possível usar a hierarquia de nós e os detalhes na tabela NODE_DISTRIBUTION para desviar caminhos individuais na rede neural e exibir estatísticas da camada oculta. Para obter mais informações, consulte [exemplos de consulta de modelo de rede Neural](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 [Voltar ao Início](#bkmk_NNviewer)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Adicionando um modelo de regressão logística à estrutura do Call Center &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo do modelo de mineração para modelos de rede neural &#40;Analysis Services – Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Exemplos de consulta de modelo de rede neural](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Microsoft Neural Network Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Alterar a diferenciação de uma coluna em um modelo de mineração](../../2014/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)  
  
  
