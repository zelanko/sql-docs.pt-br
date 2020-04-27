---
title: Algoritmo do Microsoft Time Series | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- algorithms [data mining]
- cross predictions
- series [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 642297cc-f32a-499b-b26e-fdc7ee24361e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97132ff64405df19c56c080cc5a1baa704a700d3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083764"
---
# <a name="microsoft-time-series-algorithm"></a>Algoritmo MTS
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo Time Series fornece algoritmos de regressão que são otimizados para a previsão de valores contínuos, como vendas de produtos, ao longo do tempo. Enquanto outros algoritmos [!INCLUDE[msCoName](../../includes/msconame-md.md)] , como árvores de decisão, requerem colunas adicionais de novas informações como entrada para prever uma tendência; um modelo de série temporal não requer isso. Um modelo de série temporal pode prever tendências baseadas somente no conjunto de dados original, usado para criar o modelo. Também é possível adicionar novos dados ao modelo quando fizer uma previsão e incorporar automaticamente os novos dados na análise de tendência.  
  
 O diagrama a seguir mostra um modelo típico de previsão de vendas de um produto, em quatro regiões diferentes de vendas no decorrer do tempo. O modelo exibido no diagrama mostra as vendas efetuadas em cada região, plotadas como vermelhas, amarelas, roxas e azuis. A linha para cada região tem duas partes:  
  
-   As informações históricas são exibidas à esquerda da linha vertical e representam os dados que o algoritmo usa para criar o modelo.  
  
-   As informações previstas são exibidas à direita da linha vertical e representam a previsão que o modelo faz.  
  
 A combinação de dados de origem e dos dados de previsão é chamada de uma *série*.  
  
 ![Um exemplo de série temporal](../media/time-series.gif "Um exemplo de série temporal")  
  
 Um recurso importante do algoritmo MTS ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series) é sua capacidade de executar previsão cruzada. Se você treinar o algoritmo com duas séries separadas, mas relacionadas, será possível usar o modelo resultante para prever o resultado de uma série com base no comportamento da outra série. Por exemplo, as vendas observadas de um produto podem influenciar nas vendas previstas de outro produto. A previsão cruzada também é útil para criar um modelo geral que possa ser aplicado a várias séries. Por exemplo, as previsões para uma região específica são instáveis, porque a série não possui dados de boa qualidade. Você poderia treinar um modelo geral em uma média de todas as quatro regiões e, em seguida, aplicar o modelo à série individual para criar previsões mais estáveis para cada região.  
  
## <a name="example"></a>Exemplo  
 A equipe de gerenciamento da [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] deseja prever as vendas mensais de bicicletas do próximo ano. A empresa está especialmente interessada em saber se a venda de um modelo de bicicleta pode ser usada para prever a venda de outro modelo. Usando o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series em dados históricos dos últimos três anos, a empresa pode produzir um modelo de mineração de dados que preveja futuras vendas de bicicletas. Além disso, a empresa pode realizar previsões cruzadas para determinar se as tendências de vendas de modelos de bicicleta individuais estão relacionadas.  
  
 A empresa planeja, a cada trimestre, atualizar o modelo com dados recentes de vendas bem como as previsões relativas às tendências recentes do modelo. Para corrigir lojas que não efetuam atualizações de dados de vendas de modo preciso ou consistente, eles criarão um modelo de previsão geral e usarão isso para criar previsões para todas as regiões.  
  
## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo de série temporal usou um único algoritmo, ARTxp. O algoritmo ARTXP foi otimizado para previsões de curto prazo e, portanto, previsto o próximo valor provável em uma série. A partir [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]do, [!INCLUDE[msCoName](../../includes/msconame-md.md)] o algoritmo de série temporal usa o algoritmo ARTXP e um segundo algoritmo, ARIMA. O algoritmo ARIMA é otimizado para previsão de longo prazo. Para obter uma explicação detalhada sobre a implementação dos algoritmos ARTXP e ARIMA, consulte [Referência técnica do algoritmo MTS](microsoft-time-series-algorithm-technical-reference.md).  
  
 Por padrão, o algoritmo MTS ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series) usa uma combinação de algoritmos quando analisa padrões e realiza previsões. O algoritmo treina dois modelos separados nos mesmos dados: um modelo usa o algoritmo ARTXP e um modelo usa o algoritmo ARIMA. O algoritmo combina os resultados dos dois modelos para produzir a melhor previsão para um número variável de frações de tempo. Como o ARTXP é melhor para previsões de curto prazo, ele é mais ponderado no início de uma série de previsões. No entanto, como as frações de tempo que você está prevendo estão mais adiante no futuro, o ARIMA é mais ponderado.  
  
 Você também pode controlar a combinação de algoritmos para favorecer a previsão na série temporal a curto como a longo prazo. A partir [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] do padrão, você pode especificar que [!INCLUDE[msCoName](../../includes/msconame-md.md)] o algoritmo de série temporal use uma das seguintes configurações:  
  
-   Use o ARTXP somente para previsão a curto prazo.  
  
-   Use o ARIMA somente para previsão a longo prazo.  
  
-   Use a combinação padrão dos dois algoritmos.  
  
 A partir [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]do, você pode personalizar como [!INCLUDE[msCoName](../../includes/msconame-md.md)] o algoritmo Time Series combina os modelos de previsão. Quando você usa um modelo combinado, o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series combina os dois algoritmos do seguinte modo:  
  
-   Somente o ARTXP é usado sempre para efetuar as primeiras previsões.  
  
-   Após as primeiras previsões, uma combinação do ARIMA e ARTXP é usada.  
  
-   À medida que o número de etapas de previsão aumenta, as previsões passam a ser baseadas mais pesadamente no ARIMA, até o ponto em que o ARTXP deixa de ser usado.  
  
-   Você controla o ponto de combinação, a taxa de redução do peso do ARTXP e do aumento do peso do ARIMA, configurando o parâmetro PREDICTION_SMOOTHING.  
  
 Ambos os algoritmos podem detectar sazonalidade nos dados em vários níveis. Por exemplo, seus dados podem conter ciclos mensais aninhados nos ciclos anuais. Para detectar esses ciclos sazonais, você pode fornecer uma dica de periodicidade ou especificar que o algoritmo detecte a periodicidade automaticamente.  
  
 Além da periodicidade, há vários outros parâmetros que controlam o comportamento do algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series quando ele detecta periodicidade, realiza previsões ou analisa casos. Para obter informações sobre esse como definir parâmetros de algoritmos, consulte [Referência técnica do algoritmo MTS](microsoft-time-series-algorithm-technical-reference.md).  
  
## <a name="data-required-for-time-series-models"></a>Dados necessário para modelos da série temporal  
 Quando você preparar dados para usar em treinamento para qualquer modelo de mineração de dados, verifique se entendeu os requisitos para o modelo específico e como os dados são usados.  
  
 Cada modelo de previsão deve conter uma série de casos contendo a coluna que especifica as frações de tempo ou outras séries em que ocorrem as mudanças. Por exemplo, os dados do diagrama anterior mostram a série de vendas de bicicletas, históricas e previstas, por um período de vários meses. Para esse modelo, cada região é uma série e a coluna de data contém a série temporal, que também é a série temporal. Em outros modelos, a série temporal pode ser um campo de texto ou algum identificador, como uma ID de cliente ou ID de transação. Entretanto, o modelo de série temporal deve usar sempre uma data, hora ou algum outro valor numérico exclusivo para a série temporal.  
  
 Os requisitos para um modelo de série temporal são os seguintes:  
  
-   **Uma única coluna key time** Cada modelo deve conter uma coluna numérica ou de data que é usada como a série de casos, que define as frações de tempo que o modelo usará. O tipo de dados para a coluna Key Time pode ser do tipo de data e hora ou numérico. Entretanto, a coluna deve conter valores contínuos e os valores devem ser exclusivos para cada série. A série temporal para o modelo de série temporal não pode ser armazenada em duas colunas, como uma coluna de Ano e uma coluna de Mês.  
  
-   **Uma coluna previsível** Cada modelo deve conter pelo menos uma coluna previsível em torno da qual o algoritmo criará o modelo de série temporal. O tipo de dados na coluna previsível deve ter valores contínuos. Por exemplo, você pode prever como atributos numéricos, como renda, vendas ou tempo, mudam com o decorrer do tempo. Entretanto, não é possível usar uma coluna que contenha valores discretos, como status de compra ou nível de educação, como a coluna previsível.  
  
-   **Uma coluna da chave da série opcional** Cada modelo pode ter uma coluna da chave adicional que contém valores exclusivos que identificam uma série. A coluna da chave da série opcional deve conter valores exclusivos. Por exemplo, um único modelo pode conter vendas para muitos modelos de produto, contanto que haja somente um registro para cada nome de produto para cada fração de tempo.  
  
 Você pode definir dados de entrada para o modelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series de várias maneiras diferentes. Entretanto, como o formato dos casos de entrada afeta a definição do modelo de mineração, você deverá considerar suas necessidades comerciais e preparar os dados devidamente. Os dois exemplos a seguir ilustram como os dados de entrada afetam o modelo. Nos dois exemplos, o modelo de mineração concluído contém padrões para quatro séries distintas:  
  
-   Vendas do Produto A  
  
-   Vendas do Produto B  
  
-   Volume do Produto A  
  
-   Volume do Produto B  
  
 Nos dois exemplos, você pode prever novas vendas futuras e o volume de cada produto. Você não pode prever novos valores para o produto ou para a hora.  
  
### <a name="example-1-time-series-data-set-with-series-represented-as-column-values"></a>Exemplo 1: Conjunto de dados de série temporal com série representada como valores de coluna  
 Este exemplo usa a seguinte tabela de casos de entrada:  
  
|TimeID|Produto|Sales|Volume|  
|------------|-------------|-----------|------------|  
|1/2001|Um|1000|600|  
|2/2001|Um|1100|500|  
|1/2001|B|500|900|  
|2/2001|B|300|890|  
  
 A coluna TimeID na tabela contém um identificador de hora e tem duas entradas para cada dia. A coluna de TimeID torna-se a série temporal. Portanto, você designaria essa coluna como a de key time para o modelo de série temporal.  
  
 A coluna Product define um produto no banco de dados. Essa coluna contém a série do produto. Portanto, você designaria essa coluna como uma segunda chave para o modelo de série temporal.  
  
 A coluna Sales descreve os lucros brutos do produto especificado relativos a um dia e a coluna Volume descreve a quantidade residual do produto especificado contida no armazém. Essas duas colunas contêm os dados que são usados para treinar o modelo. Tanto Sales quanto Volume podem ser atributos previsíveis para cada série na coluna Product.  
  
### <a name="example-2-time-series-data-set-with-each-series-in-separate-column"></a>Exemplo 2: Conjunto de dados de série temporal com cada série em uma coluna separada  
 Embora este exemplo use basicamente os mesmos dados de entrada, que o primeiro exemplo, esses dados são estruturados de modo diferente, conforme mostrado na tabela seguinte:  
  
|TimeID|A_Sales|A_Volume|B_Sales|B_Volume|  
|------------|--------------|---------------|--------------|---------------|  
|1/2001|1000|600|500|900|  
|2/2001|1100|500|300|890|  
  
 Nessa tabela, a coluna TimeID ainda contém a série temporal do modelo da série temporal, no qual você designa como a coluna key time. Entretanto, as colunas anteriores de Sales e Volume agora estão divididas em duas colunas e cada uma delas é precedida pelo nome do produto. Como resultado, existe somente uma única entrada para cada dia na coluna TimeID. Isto cria um modelo de série temporal que contém quatro colunas previsíveis: A_Sales, A_Volume, B_Sales e B_Volume.  
  
 Além disso, como você separou os produtos em colunas diferentes, não é necessário especificar uma coluna de chave de série adicional. Todas as colunas no modelo são uma coluna de série de casos ou uma coluna previsível.  
  
## <a name="viewing-a-time-series-model"></a>Exibindo um modelo de série temporal  
 Depois que o modelo tiver sido treinado, os resultados serão armazenados como um conjunto de padrões, que você poderá explorar ou usar para realizar previsões.  
  
 Para explorar o modelo, você pode usar o [Visualizador MTS](browse-a-model-using-the-microsoft-time-series-viewer.md). O visualizador inclui um gráfico que exibe previsões futuras e uma exibição de árvore das estruturas periódicas dos dados.  
  
 Se desejar saber mais sobre como as previsões são calculadas, você poderá navegar pelo modelo no [Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). O conteúdo armazenado para o modelo inclui detalhes como: as estruturas periódicas detectadas pelos algoritmos ARIMA e ARTXP, a equação usada para combinar os algoritmos e outras estatísticas.  
  
## <a name="creating-time-series-predictions"></a>Criando previsões de série temporal  
 Por padrão, quando você exibe um modelo de série temporal, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mostra cinco previsões para a série. Entretanto, você pode criar consultas para retornar um número variável de previsões e adicionar colunas extras às previsões para retornar estatísticas descritivas. Para obter informações sobre como criar consultas com base em um modelo de série temporal, consulte [Exemplos de consulta de um modelo de série temporal](time-series-model-query-examples.md). Para obter exemplos de como usar as extensões DMX para efetuar previsões da série temporal, consulte [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
 Ao usar o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series para fazer previsões, você deve considerar as seguintes restrições e requisitos adicionais:  
  
-   A previsão cruzada estará disponível somente quando você usar um modelo combinado ou um modelo baseado no algoritmo ARTXP. Se você usar um modelo baseado somente no algoritmo ARIMA, a previsão cruzada não será possível.  
  
-   Um modelo de série temporal pode fazer previsões que diferem às vezes, significativamente, dependendo do sistema operacional de 64 bits que o servidor usar. Essas diferenças ocorrem devido ao modo como um sistema com base em [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]representa e lida com números para aritmética de ponto flutuante, que difere do modo de um sistema com base em [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] Como os resultados da previsão podem ser específicos para o sistema operacional, recomendamos que você avalie modelos no mesmo sistema operacional que usará na produção.  
  
## <a name="remarks"></a>Comentários  
  
-   Não suporta o uso de PMML (Predictive Model Markup Language) para criar modelos de mineração.  
  
-   Suporta o uso de modelos de mineração OLAP.  
  
-   Não suporta a criação de dimensões de mineração de dados.  
  
-   Dá suporte ao detalhamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Procurar um modelo usando o Visualizador do Microsoft Time Series](browse-a-model-using-the-microsoft-time-series-viewer.md)   
 [Referência técnica do algoritmo do Microsoft Time Series](microsoft-time-series-algorithm-technical-reference.md)   
 [Exemplos de consulta de modelo de série temporal](time-series-model-query-examples.md)   
 [Conteúdo do modelo de mineração para modelos de série temporal &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
