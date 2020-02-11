---
title: Referência técnica do algoritmo do Microsoft Time Series | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ARTXP
- HISTORICAL_MODEL_GAP parameter
- AUTO_DETECT_PERIODICITY parameter
- time series algorithms [Analysis Services]
- ARIMA
- INSTABILITY_SENSITIVITY parameter
- PERIODICITY_HINT parameter
- MAXIMUM_SERIES_VALUE parameter
- time series [Analysis Services]
- MINIMUM_SUPPORT parameter
- HISTORIC_MODEL_COUNT parameter
- FORECAST_METHOD parameter
- MISSING_VALUE_SUBSTITUTION parameter
- MINIMUM_SERIES_VALUE parameter
- COMPLEXITY_PENALTY parameter
- PREDICTION_SMOOTHING parameter
ms.assetid: 7ab203fa-b044-47e8-b485-c8e59c091271
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c5ffde59f990602964ac178e629a9967d6304d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083760"
---
# <a name="microsoft-time-series-algorithm-technical-reference"></a>Referência técnica do algoritmo MTS
  O algoritmo MTS ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series) inclui dois algoritmos separados para análise de série temporal:  
  
-   O algoritmo ARTXP, introduzido no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], foi otimizado para prever o próximo valor provável em uma série.  
  
-   O algoritmo ARIMA foi adicionado no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para melhorar a exatidão da previsão de longo prazo.  
  
 Por padrão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa cada algoritmo separadamente para treinar o modelo e, em seguida, mescla os resultados para produzir a melhor previsão para um número variável de previsões. Você também pode usar apenas um dos algoritmos com base nos seus dados e requisitos de previsão. No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)], é possível personalizar também o ponto de corte que controla a mescla de algoritmos durante a previsão.  
  
 Este tópico fornece informações adicionais sobre como cada algoritmo é implementado e como você pode personalizar o algoritmo com a configuração de parâmetros para ajustar a análise e os resultados da previsão.  
  
## <a name="implementation-of-the-microsoft-time-series-algorithm"></a>Implementação do algoritmo MTS  
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Research desenvolveu o algoritmo ARTXP original que era usado no SQL Server 2005, baseando a implementação no algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Portanto, o algoritmo ARTXP pode ser descrito como um modelo de árvore de regressão automática para representar dados de série temporal periódicos. Esse algoritmo relaciona um número variável de itens passados a cada item atual que está sendo previsto. O nome ARTXP tem origem no fato de o método de árvore de regressão automática (um algoritmo ART) ser aplicado a vários estados anteriores desconhecidos. Para obter uma explicação detalhada do algoritmo ARTXP, consulte [Autoregressive Tree Models for Time-Series Analysis](https://go.microsoft.com/fwlink/?LinkId=45966).  
  
 O algoritmo ARIMA foi adicionado ao algoritmo Microsoft Time Series no SQL Server 2008 para melhorar a previsão de longo prazo. Ele é uma implementação do processo de computação de média de movimentação integrada de regressão automática, descrito por Box e Jenkins. A metodologia ARIMA permite determinar dependências em observações feitas consecutivamente em um determinado tempo e pode incorporar choques aleatórios como parte do modelo. O método ARIMA também aceita a periodicidade multiplicativa. Leitores com interesse em saber mais sobre o algoritmo ARIMA devem ler o trabalho seminal de Box e Jenkins; esta seção visa fornecer detalhes específicos sobre como a metodologia ARIMA foi implementada no algoritmo Microsoft Time Series.  
  
 Por padrão, o algoritmo Microsoft Times Series usa os dois métodos, ARTXP e ARIMA, combinando os resultados para aumentar a precisão da previsão. Se desejar usar apenas um método específico, você poderá definir os parâmetros de algoritmo para usar apenas ARTXP ou apenas ARIMA, ou para controlar como os resultados dos algoritmos são combinados. Note que o algoritmo ARTXP dá suporte à previsão cruzada, o que não ocorre no algoritmo ARIMA. Portanto, a previsão cruzada está disponível somente quando você usa uma mescla de algoritmos ou configura um modelo para usar somente ARTXP.  
  
## <a name="understanding-arima-difference-order"></a>Compreendendo a ordem de diferença no ARIMA  
 Esta seção apresenta terminologia necessária para compreender o modelo ARIMA e aborda a implementação específica de *diferenciação* no algoritmo Microsoft Time Series. Para obter uma explicação completa desses termos e conceitos, recomenda-se consultar Box e Jenkins.  
  
-   Um termo é um componente de uma equação matemática. Por exemplo, um termo em uma equação polinomial pode incluir uma combinação de variáveis e constantes.  
  
-   A fórmula ARIMA que é incluída no algoritmo Microsoft Time Series utiliza os termos *regressão automática* e *média de movimentação* .  
  
-   Os modelos de série temporal podem ser *estáticos* ou *não estáticos*. Os *modelos estacionários* são aqueles que se revertem a uma média, embora possam ter ciclos, enquanto os modelos não- *estacionários* não têm um foco de equilíbrio e estão sujeitos a maior variação ou alteração introduzida por *choques*ou variáveis externas.  
  
-   A meta da *diferenciação* é tornar uma série temporal estável e estática.  
  
-   A  *ordem de diferença* representa o número de vezes em que a diferença entre os valores é considerada para uma série temporal.  
  
 O algoritmo Microsoft Time Series opera considerando valores em uma série de dados e tentando ajustar os dados a um padrão. Se a série de dados ainda não for estática, o algoritmo aplicará uma ordem de diferença. Quanto maior a ordem de diferença, mais estática a série temporal tenderá a ser.  
  
 Por exemplo, se você tiver a série temporal (Z1, Z2,..., Zn) e executar cálculos usando uma ordem de diferença, obterá uma nova série (y1, Y2,...., yn-1), em que *Yi = Zi +1-Zi*. Quando a ordem de diferença é 2, o algoritmo gera outra série (x1, X2,..., xn-2), com base na série y que foi derivada da equação da primeira ordem. A quantidade correta de diferenciação depende dos dados. Uma única ordem de diferenciação é mais comum em modelos que apresentam uma tendência constante; uma segunda ordem de diferenciação pode indicar uma tendência que varia com o tempo.  
  
 Por padrão, a ordem de diferenciação usada nos algoritmos Microsoft Time Series é -1; isso significa que o algoritmo detectará automaticamente o melhor valor da ordem de diferenciação. Em geral, o melhor valor é 1 (quando é necessária uma diferenciação), mas em certos casos, o algoritmo aumentará esse valor para no máximo 2.  
  
 O algoritmo Microsoft Time Series determina a ordem de diferenciação ARIMA ideal usando os valores de regressão automática. O algoritmo examine os valores AR e define um parâmetro oculto, ARIMA_AR_ORDER, que representa a ordem dos termos AR. Esse parâmetro oculto, ARIMA_AR_ORDER, tem um intervalo de valores de -1 a 8. No valor padrão -1, o algoritmo selecionará automaticamente a ordem de diferenciação adequada.  
  
 Sempre que o valor ARIMA_AR_ORDER for maior que 1, o algoritmo multiplicará a série temporal por um termo polinomial. Se um termo da fórmula polinomial for resolvido para uma raiz de 1 ou próxima de 1, o algoritmo tentará preservar a estabilidade do modelo, removendo o termo e aumentando a ordem de diferenciação em 1. Se a ordem de diferenciação já estiver no valor máximo, o termo será removido e a ordem de diferenciação não mudará.  
  
 Por exemplo, se o valor de AR = 2, o termo polinomial AR resultante poderia ser assim: 1-1,4 B +. 45B ^ 2 = (1-. 9B) (1 a 0,5 B). Observe o termo (1-. 9B) que tem uma raiz de aproximadamente 0,9. O algoritmo elimina este termo da fórmula polinomial, mas não pode aumentar a ordem de diferenciação em um pois ele já se encontra no valor máximo de 2.  
  
 Lembre-se de que a única maneira de **forçar** uma mudança na ordem de diferenciação é usando o parâmetro sem suporte, ARIMA_DIFFERENCE_ORDER. O parâmetro oculto controla quantas vezes o algoritmo faz diferenciação na série temporal, e pode ser definido digitando um parâmetro de algoritmo personalizado. Entretanto, recomenda-se alterar este valor, a menos que você esteja preparado para fazer uma experiência e esteja familiarizado com os cálculos envolvidos. Note também que no momento não existe um mecanismo, incluindo parâmetros ocultos, que o permita controlar o limite no qual o aumento na ordem de diferenciação é disparado.  
  
 Finalmente, note que a fórmula descrita antes é o caso simplificado, sem dicas de periodicidade. Se forem fornecidas dicas de periodicidade, um termo polinomial AR separado será adicionado à esquerda da equação para cada dica de periodicidade. Além disso, a mesma estratégia será aplicada para eliminar termos que possam desestabilizar a série diferenciada.  
  
## <a name="customizing-the-microsoft-time-series-algorithm"></a>Personalizando o algoritmo MTS  
 O algoritmo MTS ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series) aceita os seguintes parâmetros que afetam o comportamento, o desempenho e a exatidão do modelo de mineração resultante.  
  
> [!NOTE]  
>  O algoritmo MTS está disponível em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no entanto, alguns recursos avançados, incluindo parâmetros para personalização da análise de série temporal, têm suporte apenas em edições específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473).  
  
### <a name="detection-of-seasonality"></a>Detecção de periodicidade  
 Os algoritmos ARIMA e de ARTXP dão suporte à detecção de sazonalidade ou periodicidade. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa transformação Fast Fourier para detectar sazonalidade antes de treinar. No entanto, é possível afetar a detecção de sazonalidade e os resultados de análise de série temporal, com a definição de parâmetros de algoritmo.  
  
-   Com a alteração do valor de *AUTODETECT_SEASONALITY*, é possível influenciar o número de segmentos de tempo possíveis que são gerados.  
  
-   Com a definição de um ou de vários valores para *PERIODICITY_HINT*, é possível fornecer informações ao algoritmo sobre os ciclos esperados nos dados e potencialmente aumentar a precisão da detecção.  
  
> [!NOTE]  
>  Os algoritmos ARTXP e ARIMA são muito sensíveis a dicas de periodicidade. Portanto, fornecer uma dica incorreta pode afetar os resultados de forma adversa.  
  
### <a name="choosing-an-algorithm-and-specifying-the-blend-of-algorithms"></a>Escolhendo um algoritmo e especificando a mistura de algoritmos  
 Por padrão, ou quando você seleciona a opção de MIXED, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] combina os algoritmos e atribui o mesmo peso a eles. No entanto, no [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)], você pode especificar um algoritmo específico ou personalizar a proporção de cada algoritmo nos resultados com a configuração de um parâmetro que pondera os resultados em relação à previsão de curto ou de longo prazo. Por padrão, o parâmetro *FORECAST_METHOD* está definido como MIXED e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa os dois algoritmos e, em seguida, pondera seus valores para maximizar a intensidade de cada algoritmo.  
  
-   Para controlar a escolha do algoritmo, você define o parâmetro *FORECAST_METHOD* .  
  
-   Se desejar usar a previsão cruzada, você deve usar a opção ARTXP ou MIXED, pois o ARIMA não dá suporte a esse tipo de previsão.  
  
-   Defina o *FORECAST_METHOD* como ARTXP se você desejar favorecer a previsão a curto prazo.  
  
-   Defina o *FORECAST_METHOD* como ARIMA se você desejar melhorar a previsão a longo prazo.  
  
 No [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)], você pode personalizar também como o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mescla a combinação dos algoritmos ARIMA e ARTXP. É possível controlar o ponto inicial da mescla e a taxa de alteração definindo o parâmetro *PREDICTION_SMOOTHING* :  
  
-   Se você definir *PREDICTION_SMOOTHING* como 0, o modelo usará apenas ARTXP.  
  
-   Se você definir *PREDICTION_SMOOTHING* como 1, o modelo usará apenas ARIMA.  
  
-   Se você definir *PREDICTION_SMOOTHING* como um valor entre 0 e 1, o modelo vai ponderar o algoritmo ARTXP como uma função das etapas de previsão que diminui exponencialmente. Ao mesmo tempo, o modelo também pondera o algoritmo ARIMA como o complemento 1 do peso do ARTXP . O modelo usa a normalização e uma constante de estabilização para amenizar as curvas.  
  
 Em geral, se você prever até 5 intervalos de tempo, o ARTXP quase sempre será a melhor escolha. Porém, à medida que você aumentar o número de intervalos de tempo para previsão, o ARIMA normalmente executará melhor.  
  
 O diagrama a seguir ilustra como o modelo mescla os algoritmos quando *PREDICTION_SMOOTHING* é definido como o valor padrão, 0,5. Primeiramente, o ARIMA e o ARTXP são ponderados igualmente; mas à medida que as etapas de previsão aumentam, o ARIMA é ponderado com um peso maior.  
  
 ![curva de declínio para combinar algoritmos de série temporal](../media/time-series-mixing-default.gif "curva de declínio para combinar algoritmos de série temporal")  
  
 Em contraste, o diagrama a seguir ilustra a mesclagem dos algoritmos quando *PREDICTION_SMOOTHING* é definido como 0,2. Para a etapa [!INCLUDE[tabValue](../../includes/tabvalue-md.md)], o modelo pondera o ARIMA como 0,2 e o ARTXP como 0,8. Depois disso, o peso do ARIMA aumenta exponencialmente e o peso do ARTXP diminui exponencialmente.  
  
 ![curva de declínio para a primeira combinação de modelo de série temporal](../media/time-series-blending-curve.gif "curva de declínio para a primeira combinação de modelo de série temporal")  
  
### <a name="setting-algorithm-parameters"></a>Definindo parâmetros de algoritmo  
 A tabela a seguir descreve os parâmetros que podem ser usados com o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series:  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*AUTO_DETECT_PERIODICITY*|Especifica um valor numérico entre [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] e 1 que detecta periodicidade. O padrão é 0.6.<br /><br /> Se o valor for mais próximo a [!INCLUDE[tabValue](../../includes/tabvalue-md.md)], a periodicidade será detectada somente para dados fortemente periódicos.<br /><br /> Definir esse valor mais próximo a 1 favorece a descoberta de vários padrões que são praticamente periódicos e a geração automática de dicas de periodicidade.<br /><br /> Observação: lidar com muitas dicas de periodicidade provavelmente resultará em tempo de treinamento de modelos significativamente maior, mas também em modelos mais precisos.|  
|*COMPLEXITY_PENALTY*|Controla o crescimento da árvore de decisão. O padrão é 0.1.<br /><br /> Diminuir esse valor aumenta a chance de uma divisão. Aumentar esse valor diminui a chance de uma divisão.<br /><br /> Observação: esse parâmetro está disponível apenas em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*FORECAST_METHOD*|Especifica qual algoritmo deve ser usado para análise e previsão. Os valores possíveis são ARTXP, ARIMA e MIXED. O padrão é MIXED.|  
|*HISTORIC_MODEL_COUNT*|Especifica o número de modelos de histórico que será criado. O padrão é 1.<br /><br /> Observação: esse parâmetro está disponível apenas em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*HISTORICAL_MODEL_GAP*|Especifica o intervalo de tempo entre dois modelos de histórico consecutivos. O padrão é 10. O valor representa um número de unidades de tempo, onde a unidade é definida pelo modelo.<br /><br /> Por exemplo, a configuração desse valor como g resulta na criação de modelos de histórico para dados truncados por frações de tempo em intervalos de g, 2*g, 3\*g e assim por diante.<br /><br /> Observação: esse parâmetro está disponível apenas em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*INSTABILITY_SENSITIVITY*|Controla o ponto no qual a variância de previsão excede determinado limite, depois do qual o algoritmo ARTXP suprime previsões. O valor padrão é 1.<br /><br /> Observação: esse parâmetro não se aplica a modelos que usam apenas ARIMA.<br /><br /> O valor padrão de 1 fornece o mesmo comportamento como no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] monitora o desvio padrão normalizado para cada previsão. Assim que esse valor excede o limite de qualquer previsão, o algoritmo de série temporal retorna NULL e interrompe o processo de previsão.<br /><br /> Um valor de [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] interrompe a detecção de instabilidade. Isso significa que você pode criar um número infinito de previsões, independentemente da variação.<br /><br /> Observação: esse parâmetro pode ser modificado somente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa somente o valor padrão 1.|  
|*MAXIMUM_SERIES_VALUE*|Especifica o valor máximo para usar em previsões. Esse parâmetro é usado, junto com *MINIMUM_SERIES_VALUE*, para restringir as previsões a algum intervalo esperado. Por exemplo, você pode especificar que a quantidade de vendas prevista para qualquer dia nunca deve exceder o número de produtos no inventário.<br /><br /> Observação: esse parâmetro está disponível apenas em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*MINIMUM_SERIES_VALUE*|Especifica o valor mínimo que pode ser previsto. Esse parâmetro é usado, juntamente com *MAXIMUM_SERIES_VALUE*, para restringir as previsões a algum intervalo esperado. Por exemplo, você pode especificar que a quantidade de vendas prevista nunca deve ser um número negativo.<br /><br /> Observação: esse parâmetro está disponível apenas em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*MINIMUM_SUPPORT*|Especifica o número mínimo de intervalos de tempo necessário para gerar uma divisão em cada árvore de série temporal. O padrão é 10.|  
|*MISSING_VALUE_SUBSTITUTION*|Especifica como falhas em dados do histórico são resolvidas. Por padrão, não são permitidas falhas nos dados. Se seus dados contêm várias séries, as séries também não podem ter extremidades desbalanceadas. Isso quer dizer que todas as séries devem ter os mesmos pontos de início e de extremidade. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também usa o valor desse parâmetro para preencher as falhas em novos dados quando você realiza uma `PREDICTION JOIN` no modelo de série temporal. A tabela a seguir lista os possíveis valores para esse parâmetro:<br /><br /> Nenhum: padrão Substitui valores ausentes por valores plotados ao longo da curva do modelo treinado.<br /><br /> Anterior: repete o valor do intervalo da fração de tempo anterior.<br /><br /> Média: usa uma média de movimentação de intervalos de tempo usada no treinamento.<br /><br /> Constante numérica: usa o número especificado para substituir todos os valores ausentes.|  
|*PERIODICITY_HINT*|Fornece uma dica para o algoritmo sobre a periodicidade dos dados. Por exemplo, se as vendas variam de acordo com o ano e a unidade de medida da série são meses, a periodicidade é 12. O parâmetro assume o formato de {n [, n]}, em que n é qualquer número positivo.<br /><br /> O n nos colchetes [] é opcional e pode ser repetido sempre que necessário. Por exemplo, para criar várias dicas de periodicidade para dados fornecidos mensalmente, você pode inserir {12, 3, 1} para detectar parâmetros para o ano, trimestre e mês. Entretanto, a periodicidade tem um efeito mais visível na qualidade do modelo. Se a dica que você dá diferir da periodicidade atual, seus resultados poderão ser afetados adversamente.<br /><br /> O padrão é {1}.<br /><br /> Observação: as chaves são obrigatórias. Além disso, esse parâmetro tem um tipo de dados de cadeia de caracteres. Com isso, se você digitar esse parâmetro como parte de uma instrução DMX (Data Mining Extensions), deve colocar o número e as chaves entre aspas.|  
|*PREDICTION_SMOOTHING*|Especifica como o modelo deveria ser mesclado para otimizar a previsão. Esse parâmetro está disponível em algumas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode digitar qualquer valor entre [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] e 1 ou pode usar um dos seguintes valores:<br /><br /> 
  [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]: especifica que a previsão usa somente ARTXP. A previsão é otimizada para poucos casos.<br /><br /> 0,5: (padrão) especifica que, para previsão, ambos os algoritmos devem ser usados e os resultados são mesclados.<br /><br /> 1: Especifica que a previsão usa somente ARIMA. A previsão é otimizada para vários casos.<br /><br /> <br /><br /> Observação: Use o parâmetro *FORECAST_METHOD* para controlar o treinamento.|  
  
### <a name="modeling-flags"></a>Sinalizadores de modelagem  
 O algoritmo MTS ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series) oferece suporte aos seguintes sinalizadores de modelagem. Ao criar um modelo ou uma estrutura de mineração, você define sinalizadores de modelagem para especificar como os valores em cada coluna são manipulados durante a análise. Para obter mais informações, consulte [Sinalizadores de modelagem &#40;Mineração de dados&#41;](modeling-flags-data-mining.md).  
  
|Sinalizador de modelagem|DESCRIÇÃO|  
|-------------------|-----------------|  
|NOT NULL|Indica que a coluna não pode conter um nulo. Um erro ocorrerá se o Analysis Services encontrar um valor nulo durante o treinamento do modelo.<br /><br /> Aplica-se às colunas de estrutura de mineração.|  
|MODEL_EXISTENCE_ONLY|Significa que a  coluna será tratada como tendo dois estados possíveis: Ausente e Existente. Nulo é um valor ausente.<br /><br /> Aplica-se às colunas de modelo de mineração.|  
  
## <a name="requirements"></a>Requisitos  
 Um modelo de série temporal deve conter uma coluna Key Time com valores únicos, colunas de entrada e, pelo menos, uma coluna previsível.  
  
### <a name="input-and-predictable-columns"></a>Colunas de entrada e colunas previsíveis  
 O algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series oferece suporte a tipos de conteúdo da coluna de entrada, tipos de conteúdo da coluna previsível e sinalizadores de modelagem específicos, relacionados na tabela a seguir:  
  
|Coluna|Tipos de conteúdo|  
|------------|-------------------|  
|Atributo de entrada|Continuous, Key, Key Time e Table|  
|Atributo previsível|Continuous e Table|  
  
> [!NOTE]  
>  Os tipos de conteúdo Cíclico e Ordenado têm suporte, mas o algoritmo os trata como valores discretos e não executa processamento especial.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmo do Microsoft Time Series](microsoft-time-series-algorithm.md)   
 [Exemplos de consulta de modelo de série temporal](time-series-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos de série temporal &#40;mineração de dados Analysis Services&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
