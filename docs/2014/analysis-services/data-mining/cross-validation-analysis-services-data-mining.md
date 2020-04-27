---
title: Validação cruzada (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
- scoring [data mining]
- accuracy testing [data mining]
ms.assetid: 718b9072-0f35-482a-a803-9178002ff5b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bde0035ae3c855d2add02003ca9ea84357146f90
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68809849"
---
# <a name="cross-validation-analysis-services---data-mining"></a>Validação cruzada (Analysis Services - Mineração de dados)
  A *validação cruzada* é uma ferramenta padrão no Analytics e é um recurso importante para ajudá-lo a desenvolver e ajustar os modelos de data mining. Você utiliza a validação cruzada depois de criar uma estrutura de mineração e os modelos de mineração relacionados para assegurar a validade do modelo.  A validação cruzada tem os aplicativos seguintes:  
  
-   Validando a robustez de um modelo de mineração particular.  
  
-   Avaliando vários modelos de uma única instrução.  
  
-   Construindo vários modelos e identificando o melhor modelo baseado em estatísticas.  
  
 Esta seção descreve como utilizar os recursos de validação cruzada fornecidos para mineração de dados e como interpretar os resultados da validação cruzada para um modelo único ou diversos modelos baseados em um conjunto de dados único.  
  
## <a name="overview-of-cross-validation-process"></a>Visão geral de processo da validação cruzada  
 A validação cruzada consiste em duas fases, treinamento e geração de resultado. Estas fases incluem as seguintes etapas:  
  
-   Selecione uma estrutura de mineração de destino.  
  
-   Especifique os modelos que você quer testar. Esta etapa é opcional; você também pode testar apenas a estrutura de mineração.  
  
-   Especifique os parâmetros por testar os modelos treinados.  
  
    -   O atributo previsível, valor previsto e limiar de exatidão.  
  
    -   O número de dobras nas qual dividir os dados de estrutura ou modelo.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria e treina tantos modelos quanto há dobras.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna um conjunto de métricas de precisão para cada dobra em cada modelo ou para o conjunto de dados como um todo.  
  
## <a name="configuring-cross-validation"></a>Configurando a validação cruzada  
 Você pode personalizar a forma como a validação cruzada funciona para controlar o número de seções cruzadas, os modelos testados e a barra de exatidão para as previsões. Se você utilizar os procedimentos armazenados de validação cruzada, também poderá especificar o conjunto de dados que é usado para validar os modelos. Essa riqueza de opções significa que você pode facilmente produzir muitos conjuntos de resultados diferentes que devem ser comparados e analisados.  
  
 Esta seção fornece informações para ajudar a configurar a validação cruzada adequadamente.  
  
### <a name="setting-the-number-of-partitions"></a>Definindo o número de partições  
 Quando você especifica o número de partições, determina quantos modelos temporários serão criados. Para cada partição, uma seção cruzada dos dados é sinalizada para ser utilizada como o conjunto de teste, e um novo modelo é criado pelo treinamento nos dados restantes e não na partição. Este processo está repetido até que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenha criado e testado o número especificado de modelos. Os dados que você especificou como estando disponível para validação cruzada são distribuídos uniformemente entre todas as partições.  
  
 O exemplo no diagrama ilustrará o uso de dados se forem especificadas três dobras.  
  
 ![Como executar a validação cruzada de dados de segmento](../media/xvoverviewmain.gif "Como executar a validação cruzada de dados de segmento")  
  
 No cenário do diagrama, a estrutura de mineração contém um conjunto de dados de validação que é utilizado para teste, mas o conjunto de dados de teste não foi incluído para validação cruzada. Como resultado, todos os dados no conjunto de dados de treinamento, 70% dos dados na estrutura de mineração, são utilizados para validação cruzada. O relatório da validação cruzada mostra o número total de casos usados em cada partição.  
  
 Você também pode especificar a quantidade de dados que é utilizada durante a validação cruzada, especificando o número total de casos a serem utilizados. Os casos são distribuídos uniformemente por todas as dobras.  
  
 Para as estruturas de mineração armazenadas em uma instância do SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o valor máximo que você pode definir para o número de dobras será 256, ou o número de casos, o que for menor. Se você estiver usando uma estrutura de mineração de sessão, o número de máximo de dobras será 10.  
  
> [!NOTE]  
>  À medida que você aumenta o número de dobras, o tempo necessário para executar a validação cruzada também aumenta, porque um modelo deve ser gerado e testado para cada dobra. Você poderá experimentar problemas de desempenho se o número de dobras for muito alto.  
  
### <a name="setting-the-accuracy-threshold"></a>Definir o limite de precisão  
 O limiar de estado permite definir a barra de exatidão para previsões. Para cada caso, o modelo calcula a *probabilidade de previsão*, significando a probabilidade de o estado previsto estar correto. Se a probabilidade de previsão exceder a barra de exatidão, a previsão é considerada correta; caso contrário, a previsão é considerada incorreta. Você controla esse valor, definindo **Limiar de Estado** para um número entre 0,0 e 1,0, em que os números mais próximos de 1 indicam um grande nível de confiança nas previsões, e os números próximos a 0 indicam que a previsão tem menor probabilidade de ser verdadeira. O valor padrão para o limiar de estado é NULL, o que significa que o estado previsto com a probabilidade mais alta é considerado o valor de destino.  
  
 Você deve saber que a configuração para o limite de estado afeta as medidas de exatidão do modelo. Por exemplo, suponha que você tenha três modelos que deseja testar. Todos são baseados na mesma estrutura de mineração e todos preveem a coluna [Bike Buyer]. Além disso, você deseja prever um único valor de 1, significando "sim, comprará". Os três modelos retornam previsões com probabilidade prevista de 0,05, 0,15 e 0,8. Se você definir o limiar de estado para 0,10, duas das previsões serão consideradas corretas. Se você definir o limiar de estado como 0,5, só um modelo será considerado como havendo retornado uma previsão correta. Se você usar o valor padrão, nulo, será mais provável que a previsão seja considerada correta. Neste caso, todas as três previsões seriam consideradas corretas.  
  
> [!NOTE]  
>  Você pode definir um valor de 0,0 para o limite, mas o valor não tem muito sentido, porque cada previsão será considerada correta, mesmo com a probabilidade zero. Tenha cuidado para não definir **Limiar de Estado** para 0,0.  
  
### <a name="choosing-models-and-columns-to-validate"></a>Escolher os modelos e colunas para validar  
 Ao usar a guia **Validação Cruzada** no Designer de Mineração de Dados, você deve primeiro selecionar a coluna previsível de uma lista. Normalmente, uma estrutura de mineração pode aceitar muitos modelos de mineração, porém nem todos os modelos usam a mesma coluna previsível. Ao executar a validação cruzada, só podem ser incluídos no relatório os modelos que usam a mesma coluna previsível.  
  
 Para escolher um atributo previsível, clique em **Atributo de Destino** e selecione a coluna da lista. Se o atributo de destino for uma coluna aninhada ou uma coluna em uma tabela aninhada, você deverá digitar o nome da coluna aninhada usando \<o formato nome da tabela aninhada> (chave). \<> de coluna aninhada. Se a única coluna usada da tabela aninhada for a coluna de chave, você poderá \<usar o nome de tabela aninhada> (chave).  
  
 Depois que você seleciona o atributo previsível, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] automaticamente testa todos os modelos que usam o mesmo atributo previsível. Se o atributo de destino contém valores discretos, após você ter selecionado a coluna previsível é possível informar opcionalmente um estado de destino, isto se existir um valor específico que você deseja prever.  
  
 A seleção do estado de destino afeta as medidas que são retornadas. Se você especificar um atributo de destino, ou seja, um nome de coluna, e não escolher um valor específico que você deseja que o modelo preveja, por padrão o modelo será avaliado em sua previsão do estado mais provável.  
  
 Quando você usa a validação cruzada com modelos de clustering, não existe a coluna previsível; ao invés disso, você seleciona **#Cluster** de uma lista de atributos previsíveis na caixa de listagem **Atributo de Destino** . Após você ter selecionado essa opção, outras opções que não são relevantes para modelos de clustering, como **Estado de Destino**serão desabilitadas. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] testará todos os modelos de clustering associados com a estrutura de mineração.  
  
## <a name="tools-for-cross-validation"></a>Ferramentas para a validação cruzada  
 Você também pode usar a validação cruzada do Designer de Mineração de Dados ou pode realizar validação cruzada executando os procedimentos armazenados.  
  
 Se você usar as ferramentas do Designer de Mineração de Dados para executar validação cruzada, poderá configurar os parâmetros dos resultados do treinamento e da exatidão em uma única caixa de diálogo. Isto torna mais fácil configurar e exibir os resultados. Você pode medir a exatidão de todos os modelos de mineração que estão relacionados a uma única estrutura de mineração e exibir imediatamente os resultados em um relatório HTML. Porém, os procedimentos armazenados oferecem algumas vantagens, como as personalizações adicionadas e a capacidade de criar script do processo.  
  
### <a name="cross-validation-in-data-mining-designer"></a>Validação cruzada no Designer de Mineração de Dados  
 Você pode executar a validação cruzada usando a guia **Validação Cruzada** da exibição Gráfico de Precisão de Mineração no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no SQL Server Development Studio.  
  
 Para ver um exemplo de como criar um relatório de validação cruzada usando a interface do usuário, consulte [Criar um relatório de validação cruzada](create-a-cross-validation-report.md).  
  
### <a name="cross-validation-stored-procedures"></a>Procedimentos armazenados da validação cruzada  
 Para usuários avançados, a validação cruzada também está disponível na forma de procedimentos armazenados do sistema parametrizados completamente. Você pode executar os procedimentos armazenados conectando-se a uma instância do [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] a partir do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou de qualquer aplicativo de código gerenciado.  
  
 Os procedimentos armazenados são agrupados pelo tipo de modelo de mineração. Um conjunto de procedimentos armazenados trabalha apenas com modelos de clustering. O outro conjunto de procedimentos armazenados trabalha com outros modelos de mineração.  
  
 Para cada tipo de modelo de mineração, clusterizado ou não clusterizado, os procedimentos armazenados executam validação cruzada em duas fases separadas.  
  
 **Particiona dados e gera métricas para partições**  
  
 Para a primeira fase, você chama um procedimento armazenado do sistema que cria quantas partições você especificar dentro do conjunto de dados e retorna resultados de exatidão para cada partição. Para cada métrica, o Analysis Services então calcula o desvio médio e o padrão para as partições.  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](/sql/analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](/sql/analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining)  
  
 **Gere métrica para o conjunto de dados inteiro**  
  
 Na segunda fase, você chama um conjunto diferente de procedimentos armazenados. Esses procedimentos armazenados não particionam o conjunto de dados, mas geram resultados de exatidão para o conjunto de dados especificado como um todo. Se você já dividiu e processou uma estrutura de mineração, poderá chamar este segundo conjunto de procedimentos armazenados para obter apenas os resultados.  
  
-   [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](/sql/analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](/sql/analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining)  
  
#### <a name="defining-the-testing-data"></a>Definindo os dados de teste  
 Quando você executa os procedimentos armazenados de validação cruzada que calculam a precisão, (SystemGetAccuracyResults or SystemGetClusterAccuracyResults), pode especificar a fonte dos dados que é utilizada para teste, durante a validação cruzada. Essa opção não está disponível na interface de usuário.  
  
 Você pode especificar como uma fonte de dados de teste qualquer uma das seguintes opções:  
  
-   Use só os dados de treinamento.  
  
-   Inclua um conjunto de dados de teste existente.  
  
-   Use só o conjunto de dados de teste.  
  
-   Aplique os filtros existentes a cada modelo.  
  
-   Qualquer combinação de conjunto de treinamento, conjunto de teste e filtros de modelo.  
  
 Para especificar uma fonte de dados de testes, você fornece um valor inteiro para o parâmetro `DataSet` do procedimento armazenado. Para obter uma lista de valores de argumento, consulte a seção Comentários do tópico correspondente de referência dos procedimentos armazenados.  
  
 Se você executar a validação cruzada usando o relatório **Validação Cruzada** no Designer de Mineração de Dados, não poderá alterar o conjunto de dados que é usado. Por padrão, os casos de treinamento para cada modelo são usados. Se um filtro estiver associado a um modelo, o filtro será aplicado.  
  
## <a name="results-of-cross-validation"></a>Resultados de validação cruzada  
 Se você usar o Designer de Mineração de Dados, estes resultados serão exibidos em um visualizador de Web como grade. Se você usar os procedimentos armazenados de validação cruzada, estes mesmos resultados serão retornados como uma tabela.  
  
 O relatório contém dois tipos de medidas: agregações que indicam a variabilidade do conjunto de dados quando divididas em dobras, e medidas específicas de modelo de exatidão para cada dobra. Os tópicos a seguir fornecem mais informações sobre essas métricas.  
  
 [Fórmulas de validação cruzada](cross-validation-formulas.md)  
  
 Lista todas as medidas por tipo de teste. Descreve em geral como as medidas podem ser interpretadas.  
  
 [Medidas no relatório de validação cruzada](measures-in-the-cross-validation-report.md)  
  
 Descreve as fórmulas para calcular cada medida e lista o tipo de atributo ao qual cada medida pode ser aplicada.  
  
## <a name="restrictions-on-cross-validation"></a>Restrições em validação cruzada  
 Ao executar a validação cruzada usando o relatório de validação cruzada no SQL Server Development Studio, existem algumas limitações nos modelos que você pode testar e os parâmetros que você pode configurar.  
  
-   Por padrão, todos os modelos associados com a estrutura de mineração selecionada são validados pela validação cruzada. Você não pode especificar o modelo ou uma lista de modelos.  
  
-   A Validação Cruzada não é fornecida para modelos que são baseados no algoritmo MTS ou no algoritmo MSC.  
  
-   O relatório não pode ser criado se sua estrutura de mineração não contém nenhum modelo que possa ser testado pela validação cruzada.  
  
-   Se a estrutura de mineração contém modelos de clustering e de não clustering e você não escolheu a opção **#Cluster** , os resultados para ambos os tipos de modelos são mostrados no mesmo relatório, mesmo que o atributo, o estado e as configurações de limites possam não ser apropriados para os modelos de clustering.  
  
-   Alguns valores de parâmetros são restringidos. Por exemplo, um aviso aparece se o numero de dobras for maior que 10, porque ao gerar muitos modelos o relatório pode ser exibido lentamente.  
  
 Se você estiver testando vários modelos de mineração, e os modelos tiverem filtros, cada modelo será filtrado separadamente. Você não pode adicionar um filtro a um modelo nem alterar o filtro para um modelo durante validação cruzada.  
  
 Como a validação cruzada, por padrão, testa todos os modelos de mineração associados a uma estrutura, você poderá receber resultados inconsistentes se alguns modelos tiverem um filtro e outros não. Para garantir que você compare somente aqueles modelos que têm o mesmo filtro, utilize os procedimentos armazenados e especifique uma lista dos modelos de mineração. Ou utilize somente o teste da estrutura de mineração definido como sem-filtros para garantir que um conjunto de dados consistente seja utilizado para todos os modelos.  
  
 Se você executar a validação cruzada usando os procedimentos armazenados, terá a opção adicional de escolher a origem dos dados de teste. Se você executar a validação cruzada usando o Designer de Mineração de Dados, deverá usar o conjunto de dados de testes que está associado ao modelo ou estrutura, se houver. Geralmente, se você quiser especificar configurações avançadas, deverá usar os procedimentos armazenados de validação cruzada.  
  
 A validação cruzada não pode ser usada com série temporal ou modelos de clustering de sequência. Especificamente, nenhum modelo que contém uma coluna KEY TIME ou KEY SEQUENCE pode ser incluído na validação cruzada.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Consulte os tópicos a seguir para obter mais informações sobre validação cruzada ou informações sobre métodos relacionados para testar modelos de mineração, como gráficos de exatidão.  
  
|Tópicos|Links|  
|------------|-----------|  
|Descreve como definir parâmetros de validação cruzada no SQL Server Development Studio.|[Guia Validação Cruzada &#40;Exibição do gráfico de precisão de mineração&#41;](../cross-validation-tab-mining-accuracy-chart-view.md)|  
|Descreve a métrica que é fornecida através de validação cruzada|[Fórmulas de validação cruzada](cross-validation-formulas.md)|  
|Explica o formato de relatório de validação cruzada e define as medidas estatísticas fornecidas para cada tipo de modelo.|[Medidas no relatório de validação cruzada](measures-in-the-cross-validation-report.md)|  
|Lista os procedimentos armazenados para computar estatísticas de validação cruzada.|[Procedimentos armazenados da mineração de dados &#40;Analysis Services – Mineração de dados&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)|  
|||  
|Descreve como criar um conjunto de dados de testes para estruturas de mineração e modelos relacionados.|[Conjuntos de dados de teste e treinamento](training-and-testing-data-sets.md)|  
|Consulte exemplos de outros tipos de gráfico de exatidão.|[Matriz de classificação &#40;Analysis Services – Mineração de dados&#41;](classification-matrix-analysis-services-data-mining.md)<br /><br /> [Gráfico de comparação de precisão &#40;Analysis Services – Mineração de dados&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de ganho &#40;Analysis Services – Mineração de dados&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [Dispersão &#40;Analysis Services – Mineração de dados&#41;](scatter-plot-analysis-services-data-mining.md)|  
|Descreve as etapas para criar vários gráficos de exatidão.|[Tarefas de teste e validação e instruções &#40;Mineração de dados&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Teste e validação &#40;Mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
  
