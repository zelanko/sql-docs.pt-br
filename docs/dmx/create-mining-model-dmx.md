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
manager: kfile
ms.openlocfilehash: 0e7ca6765ee44201badc54d15fb2a20aa9a863a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62853473"
---
# <a name="create-mining-model-dmx"></a>CRIAR UM MODELO DE MINERAÇÃO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cria um novo modelo de mineração e uma nova estrutura de mineração no banco de dados. É possível criar um modelo definindo o novo modelo na instrução ou usando o PMML (Predictive Model Markup Language). Essa segunda opção é apenas para usuários avançados.  
  
 A estrutura de mineração recebe o nome anexando "_structure" ao nome do modelo, o que garante que o nome da estrutura seja diferente do nome do modelo.  
  
 Para criar um modelo de mineração para uma estrutura de mineração existente, use o [ALTER MINING STRUCTURE &#40;DMX&#41; ](../dmx/alter-mining-structure-dmx.md) instrução.  
  
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
  
 *algorithm*  
 O nome de um algoritmo de mineração de dados, conforme definido pelo provedor atual.  
  
> [!NOTE]  
>  Uma lista dos algoritmos suportados pelo provedor atual pode ser recuperada por meio [conjunto de linhas DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Para exibir os algoritmos suportados na instância atual do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], consulte [propriedades de Data Mining](../analysis-services/server-properties/data-mining-properties.md).  
  
 *lista de parâmetros*  
 Opcional. Uma lista separada por vírgulas de parâmetros definidos pelo provedor para o algoritmo.  
  
 *Cadeia de caracteres XML*  
 (Apenas para uso avançado.) Um codificada em XML modelo (PMML). A cadeia deve estar entre aspas simples (').  
  
 O **sessão** cláusula permite que você crie um modelo de mineração removido automaticamente do servidor quando a conexão é fechada ou a sessão expira. **SESSÃO** modelos de mineração são úteis porque eles não exigem que o usuário seja um administrador de banco de dados e possa apenas usar espaço em disco para desde que a conexão está aberta.  
  
 O **WITH DRILLTHROUGH** cláusula habilita o detalhamento no modelo de mineração novo. O detalhamento pode ser habilitado somente durante a criação do modelo. Para alguns tipos de modelo, o detalhamento é necessário para procurar o modelo no visualizador personalizado. O detalhamento não é necessário para previsão ou para procurar o modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft.  
  
 O **CREATE MINING MODEL** instrução cria um novo modelo de mineração que se baseia a lista de definições de coluna, o algoritmo e a lista de parâmetros de algoritmo.  
  
### <a name="column-definition-list"></a>Lista de definições de coluna  
 Você define a estrutura de um modelo que usa a lista de definições da coluna incluindo as seguintes informações para cada coluna:  
  
-   Nome (obrigatório)  
  
-   Tipo de dados (obrigatório)  
  
-   Distribuição  
  
-   Lista de sinalizadores de modelagem  
  
-   Tipo de conteúdo (obrigatório)  
  
-   Solicitação de previsão, que indica ao algoritmo para prever esta coluna, indicada pela **PREDICT** ou **PREDICT_ONLY** cláusula  
  
-   Relação com uma coluna de atributo (obrigatório apenas se aplicável), indicada pela **RELATED TO** cláusula  
  
 Use a seguinte sintaxe para a lista de definições de coluna, para definir uma única coluna:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 Use a seguinte sintaxe para a lista de definições de coluna, para definir uma coluna de tabela aninhada:  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 Exceto para os sinalizadores de modelagem, não é possível usar mais de uma cláusula de um grupo específico para definir uma coluna. É possível definir diversos sinalizadores de modelagem para uma coluna.  
  
 Para obter uma lista dos tipos de dados, dos tipos de conteúdo, de distribuições de coluna e de sinalizadores de modelagem que podem ser usados para definir uma coluna, consulte os seguintes tópicos:  
  
-   [Tipos de dados &#40;Mineração de dados&#41;](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [Tipos de conteúdo &#40;Data Mining&#41;](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [Distribuições de colunas &#40;Mineração de dados&#41;](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [Sinalizadores de modelagem &#40;Mineração de dados&#41;](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 É possível adicionar uma cláusula a instrução para descrever a relação entre duas colunas. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte ao uso dos seguintes \<Column relationship > cláusula.  
  
 **RELACIONADOS A**  
 Este formulário indica uma hierarquia de valor. O destino de uma coluna RELATED TO pode ser a coluna de chave em uma tabela aninhada, uma coluna com um valor discreto na linha de caso ou outra coluna com uma cláusula RELATED TO, que indica uma hierarquia mais profunda.  
  
 Use uma cláusula de previsão para descrever como a coluna de previsão é usada. A seguinte tabela descreve as duas possíveis cláusulas.  
  
|\<Previsão > cláusula|Descrição|  
|---------------------------|-----------------|  
|**PREDICT**|Esta coluna pode ser prevista pelo modelo e pode ser fornecida em casos de entrada para prever o valor de outras colunas de previsão.|  
|**PREDICT_ONLY**|Esta coluna pode ser prevista pelo modelo, mas seus valores não podem ser usados em casos de entrada para prever o valor de outras colunas de previsão.|  
  
### <a name="parameter-definition-list"></a>Lista de definições de parâmetro  
 Você pode usar a lista de parâmetros para ajustar o desempenho e a funcionalidade de um modelo de mineração. A sintaxe da lista de parâmetros é a seguinte:  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
 Para obter uma lista dos parâmetros que estão associados com cada algoritmo, consulte [algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="remarks"></a>Comentários  
 Se você desejar criar um modelo que tem um conjunto de dados de teste interno, deverá usar a instrução CREATE MINING STRUCTURE seguida por ALTER MINING STRUCTURE. No entanto nem todos os tipos de modelo oferecem suporte a um conjunto de dados de validação. Para obter mais informações, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para obter uma explicação de como criar um modelo de mineração usando a instrução CREATEMODEL, consulte [Tutorial de DMX de previsão de série temporal](https://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2).  
  
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
 O seguinte exemplo usa o algoritmo de associação da [!INCLUDE[msCoName](../includes/msconame-md.md)] para criar um novo modelo de mineração. A instrução aproveita a capacidade de aninhar uma tabela dentro da definição do modelo usando uma coluna de tabelas. O modelo é modificado usando o *MINIMUM_PROBABILITY* e *MINIMUM_SUPPORT* parâmetros.  
  
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
 O seguinte exemplo usa o algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Times Series para criar um novo modelo de mineração usando o algoritmo ARTxp. ReportingDate é a coluna de chave para a série temporal e ModelRegion é a coluna de chave para a série de dados. Neste exemplo, presume-se que a periodicidade dos dados é a cada 12 meses. Portanto, o *PERIODICITY_HINT* parâmetro for definido como 12.  
  
> [!NOTE]  
>  Você deve especificar o *PERIODICITY_HINT* parâmetro usando caracteres de chave. Além disso, como o valor é uma cadeia de caracteres, ela deve ser colocada entre aspas simples: "{\<valor numérico >}".  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
