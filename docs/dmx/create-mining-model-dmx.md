---
title: CRIAR MODELO DE MINERAÇÃO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e7215f50705b593130a69cfe076f0878b0ac03d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68889073"
---
# <a name="create-mining-model-dmx"></a>CRIAR UM MODELO DE MINERAÇÃO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cria um novo modelo de mineração e uma nova estrutura de mineração no banco de dados. É possível criar um modelo definindo o novo modelo na instrução ou usando o PMML (Predictive Model Markup Language). Essa segunda opção é apenas para usuários avançados.  
  
 A estrutura de mineração recebe o nome anexando "_structure" ao nome do modelo, o que garante que o nome da estrutura seja diferente do nome do modelo.  
  
 Para criar um modelo de mineração para uma estrutura de mineração existente, use a instrução [ALTER MINING structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE [SESSION] MINING MODEL <model>  
(  
    [(<column definition list>)]  
)  
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH]  
CREATE MINING MODEL <model> FROM PMML <xml string>  
```  
  
## <a name="arguments"></a>Argumentos  
 *modelo*  
 Um nome exclusivo para o modelo.  
  
 *lista de definições de coluna*  
 Uma lista de definições de coluna separadas por vírgulas.  
  
 *algoritmo*  
 O nome de um algoritmo de mineração de dados, conforme definido pelo provedor atual.  
  
> [!NOTE]  
>  Uma lista dos algoritmos com suporte pelo provedor atual pode ser recuperada usando [DMSCHEMA_MINING_SERVICES conjunto de linhas](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Para exibir os algoritmos com suporte na instância atual [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]do, consulte [Propriedades de mineração de dados](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties).  
  
 *lista de parâmetros*  
 Opcional. Uma lista separada por vírgulas de parâmetros definidos pelo provedor para o algoritmo.  
  
 *Cadeia de caracteres XML*  
 (Somente para uso avançado.) Um modelo codificado em XML (PMML). A cadeia deve estar entre aspas simples (').  
  
 A cláusula **Session** permite criar um modelo de mineração que é removido automaticamente do servidor quando a conexão é fechada ou o tempo limite da sessão é atingido. Os modelos de mineração de **sessão** são úteis porque não exigem que o usuário seja um administrador de banco de dados e usam apenas espaço em disco, desde que a conexão esteja aberta.  
  
 A cláusula **WITH DRILLTHROUGH** permite Drill-through no novo modelo de mineração. O detalhamento pode ser habilitado somente durante a criação do modelo. Para alguns tipos de modelo, o detalhamento é necessário para procurar o modelo no visualizador personalizado. O detalhamento não é necessário para previsão ou para procurar o modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft.  
  
 A instrução **criar modelo de mineração** cria um novo modelo de mineração baseado na lista de definições de coluna, no algoritmo e na lista de parâmetros de algoritmo.  
  
### <a name="column-definition-list"></a>Lista de definições de coluna  
 Você define a estrutura de um modelo que usa a lista de definições da coluna incluindo as seguintes informações para cada coluna:  
  
-   Nome (obrigatório)  
  
-   Tipo de dados (obrigatório)  
  
-   Distribuição  
  
-   Lista de sinalizadores de modelagem  
  
-   Tipo de conteúdo (obrigatório)  
  
-   Solicitação de previsão, que indica ao algoritmo para prever essa coluna, indicada pela cláusula **Predict** ou **PREDICT_ONLY**  
  
-   Relação com uma coluna de atributo (obrigatória somente se aplicável), indicada pela cláusula **to relacionada**  
  
 Use a sintaxe a seguir para a lista definição de coluna, para definir uma única coluna:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 Use a sintaxe a seguir para a lista definição de coluna, para definir uma coluna de tabela aninhada:  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 Exceto para os sinalizadores de modelagem, não é possível usar mais de uma cláusula de um grupo específico para definir uma coluna. É possível definir diversos sinalizadores de modelagem para uma coluna.  
  
 Para obter uma lista dos tipos de dados, dos tipos de conteúdo, de distribuições de coluna e de sinalizadores de modelagem que podem ser usados para definir uma coluna, consulte os seguintes tópicos:  
  
-   [Tipos de dados &#40;mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-types-data-mining)  
  
-   [Tipos de conteúdo &#40;mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)  
  
-   [Distribuições de coluna &#40;mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [Sinalizadores de modelagem &#40;mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/modeling-flags-data-mining)  
  
 É possível adicionar uma cláusula a instrução para descrever a relação entre duas colunas. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]dá suporte ao uso da seguinte \<cláusula de> de relação de coluna.  
  
 **RELACIONADO A**  
 Este formulário indica uma hierarquia de valor. O destino de uma coluna RELATED TO pode ser a coluna de chave em uma tabela aninhada, uma coluna com um valor discreto na linha de caso ou outra coluna com uma cláusula RELATED TO, que indica uma hierarquia mais profunda.  
  
 Use uma cláusula de previsão para descrever como a coluna de previsão é usada. A seguinte tabela descreve as duas possíveis cláusulas.  
  
|\<cláusula de> de previsão|DESCRIÇÃO|  
|---------------------------|-----------------|  
|**PREDICT**|Esta coluna pode ser prevista pelo modelo e pode ser fornecida em casos de entrada para prever o valor de outras colunas de previsão.|  
|**PREDICT_ONLY**|Esta coluna pode ser prevista pelo modelo, mas seus valores não podem ser usados em casos de entrada para prever o valor de outras colunas de previsão.|  
  
### <a name="parameter-definition-list"></a>Lista de definições de parâmetro  
 Você pode usar a lista de parâmetros para ajustar o desempenho e a funcionalidade de um modelo de mineração. A sintaxe da lista de parâmetros é a seguinte:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
 Para obter uma lista dos parâmetros associados a cada algoritmo, consulte [algoritmos de mineração de dados &#40;&#41;de mineração de dados Analysis Services ](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
## <a name="remarks"></a>Comentários  
 Se você desejar criar um modelo que tem um conjunto de dados de teste interno, deverá usar a instrução CREATE MINING STRUCTURE seguida por ALTER MINING STRUCTURE. No entanto nem todos os tipos de modelo oferecem suporte a um conjunto de dados de validação. Para obter mais informações, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para obter uma explicação de como criar um modelo de mineração usando a instrução CREATEMODEL, consulte [tutorial DMX de previsão de série temporal](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
## <a name="naive-bayes-example"></a>Exemplo de Naive Bayes  
 O exemplo seguinte usa o algoritmo do Naive Bayes [!INCLUDE[msCoName](../includes/msconame-md.md)] para criar um novo modelo de mineração. A coluna Bike Buyer está definida como o atributo previsível.  
  
```  
CREATE MINING MODEL [NBSample]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE PREDICT  
)  
USING Microsoft_Naive_Bayes  
```  
  
## <a name="association-model-example"></a>Exemplo de modelo de associação  
 O seguinte exemplo usa o algoritmo de associação da [!INCLUDE[msCoName](../includes/msconame-md.md)] para criar um novo modelo de mineração. A instrução aproveita a capacidade de aninhar uma tabela dentro da definição do modelo usando uma coluna de tabelas. O modelo é modificado usando os parâmetros *MINIMUM_PROBABILITY* e *MINIMUM_SUPPORT* .  
  
```  
CREATE MINING MODEL MyAssociationModel (  
    OrderNumber TEXT KEY,  
    [Products] TABLE PREDICT (  
        [Model] TEXT KEY  
    )  
)  
USING Microsoft_Association_Rules (Minimum_Probability = 0.1, MINIMUM_SUPPORT = 0.01)  
```  
  
## <a name="sequence-clustering-example"></a>Exemplo de cluster de sequência  
 O exemplo seguinte usa o algoritmo MSC da [!INCLUDE[msCoName](../includes/msconame-md.md)] para criar um novo modelo de mineração. Duas chaves são usadas para definir o modelo. A coluna OrderNumber é usada como a chave do caso e especifica pedidos individuais. A coluna LineNumber é usada como a chave de tabela aninhada e especifica a sequência na qual os itens foram adicionados a um pedido.  
  
```  
CREATE MINING MODEL BuyingSequence (  
    [Order Number] TEXT KEY,  
    [Products] TABLE   
     (  
        [Line Number] LONG KEY SEQUENCE,  
        [Model] TEXT DISCRETE PREDICT  
    )  
)  
USING Microsoft_Sequence_Clustering  
```  
  
## <a name="time-series-example"></a>Exemplo de série temporal  
 O seguinte exemplo usa o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Times Series para criar um novo modelo de mineração usando o algoritmo ARTxp. ReportingDate é a coluna de chave para a série temporal e ModelRegion é a coluna de chave para a série de dados. Neste exemplo, presume-se que a periodicidade dos dados é a cada 12 meses. Portanto, o parâmetro *PERIODICITY_HINT* é definido como 12.  
  
> [!NOTE]  
>  Você deve especificar o parâmetro *PERIODICITY_HINT* usando caracteres de chaves. Além disso, como o valor é uma cadeia de caracteres, ele deve ser colocado entre aspas simples:\<"{valor numérico>}".  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
