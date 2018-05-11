---
title: SystemGetAccuracyResults (Analysis Services – mineração de dados) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1e00663db34b352670c065b13c71df228a1acd4a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="systemgetaccuracyresults-analysis-services---data-mining"></a>SystemGetAccuracyResults (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Retorna métricas de precisão de validação cruzada para uma estrutura de mineração e todos os modelos relacionados, excluindo modelos de clustering.  
  
 Esse procedimento armazenado retorna métrica para todo o conjunto de dados como uma única partição. Para dividir o conjunto de dados em seções cruzadas e retornar métricas para cada partição, use [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Esse procedimento armazenado não tem suporte para modelos criados com o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] MTS ou o algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSC. Além disso, para modelos de clustering, você pode usar o procedimento armazenado separado, [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SystemGetAccuracyResults(<mining structure>,   
[,<mining model list>]  
,<data set>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estrutura de mineração*  
 Nome de uma estrutura de mineração no banco de dados atual.  
  
 (Obrigatória)  
  
 *lista de modelos*  
 Lista separada por vírgulas de modelos para validar.  
  
 O padrão é **nulo**. Isso significa que todos os modelos aplicáveis são usados. Quando o padrão é usado, modelos de clustering são excluídos automaticamente da lista de candidatos para processamento.  
  
 (opcional)  
  
 *conjunto de dados*  
 Um valor inteiro que indica qual partição na estrutura de mineração é usada para teste. O valor é derivado de uma máscara de bits que representa a soma dos valores seguintes, onde qualquer valor único é opcional:  
  
|||  
|-|-|  
|Casos de treinamento|0x0001|  
|Casos de teste|0x0002|  
|Filtro do modelo|0x0004|  
  
 Para obter uma lista completa de valores possíveis, consulte a seção Comentários mais adiante neste tópico.  
  
 (obrigatório)  
  
 *atributo de destino*  
 Cadeia de caracteres que contém o nome de um objeto previsível. Um objeto previsível pode ser uma coluna, coluna de tabela aninhada ou coluna de chave de tabela aninhada de um modelo de mineração.  
  
 (obrigatório)  
  
 *estado de destino*  
 Cadeia de caracteres que contém um valor específico para prever.  
  
 Se um valor for especificado, as métricas serão coletadas para aquele estado específico.  
  
 Se nenhum valor for especificado ou se nulo for especificado, as métricas serão computadas para o estado mais provável para cada previsão.  
  
 O padrão é **nulo**.  
  
 (opcional)  
  
 *limite de destino*  
 Número entre 0.0 e 1 que especifica a probabilidade mínima em que o valor de previsão foi contado como correto.  
  
 O padrão é **nulo**, o que significa que todas as previsões são contadas como corretas.  
  
 (opcional)  
  
 *test list*  
 Uma cadeia de caracteres que especifica opções de teste. Esse parâmetro é reservado para uso futuro.  
  
 (opcional)  
  
## <a name="return-type"></a>Tipo de retorno  
 O conjunto de linhas que é retornado contém pontuações para cada partição e agregações para todos os modelos.  
  
 A tabela a seguir lista as colunas retornadas por **GetValidationResults**.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|Modelo|O nome do modelo que foi testado. **Tudo** indica que o resultado é uma agregação para todos os modelos.|  
|AttributeName|O nome da coluna previsível.|  
|AttributeState|Um valor de destino na coluna previsível.<br /><br /> Se essa coluna contiver um valor, só serão coletadas métrica para o estado especificado.<br /><br /> Se esse valor não for especificado ou for nulo, as métrica são computadas para o estado mais provável para cada previsão.|  
|PartitionIndex|Denota a partição à qual o resultado se aplica.<br /><br /> Para esse procedimento, sempre 0.|  
|PartitionCases|Um inteiro que indica o número de linhas no conjunto de casos, com base no  *\<conjunto de dados >* parâmetro.|  
|Teste|O tipo de teste que foi executado.|  
|Measure|Nome da medida retornada pelo teste. Medidas para cada modelo dependem do tipo modelo e do tipo do valor previsível.<br /><br /> Para obter uma lista de medidas retornadas para cada tipo previsível, consulte [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Para obter uma definição de cada medida, consulte [Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|Value|O valor para a medida especificada.|  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir fornece exemplos dos valores que você pode usar para especificar os dados na estrutura de mineração usados para validação cruzada. Se você desejar usar casos de teste para validação cruzada, a estrutura de mineração já deverá conter um conjunto de dados para teste. Para obter informações sobre como definir um conjunto de dados de teste ao criar uma estrutura de mineração, consulte [Conjuntos de dados de treinamento e teste](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
|Valor inteiro|Description|  
|-------------------|-----------------|  
|1|Somente casos de treinamento são usados.|  
|2|Somente os casos de teste são usados.|  
|3|Somente os casos de teste e de treinamento são usados.|  
|4|Combinação inválida.|  
|5|Somente casos de teste são usados e o filtro de modelo é aplicado.|  
|6|Somente casos de teste são usados e o filtro de modelo é aplicado.|  
|7|Os casos de teste e de treinamento são usados e o filtro de modelo é aplicado.|  
  
 Para obter mais informações sobre os cenários nos quais você usaria validação cruzada, consulte [Teste e validação &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
## <a name="examples"></a>Exemplos  
 Esse exemplo retorna medidas de precisão para um único modelo da árvore de decisão, `v Target Mail DT`, que é associado com a estrutura de mineração `vTargetMail` . O código da linha quatro indica que os resultados devem ser baseados nos casos de testes, filtrados para cada modelo pelo filtro específico desse modelo.  `[Bike Buyer]` especifica a coluna que será prevista e o 1 na linha seguinte indica que o modelo só será avaliado para o valor 1 específico, significando "Sim, comprará".  
  
 A linha final do código especifica que o valor do limite de estado é 0.5. Isso significa que previsões com uma probabilidade maior que 50% devem ser contados como previsões “boas” no cálculo da previsão.  
  
```  
CALL SystemGetAccuracyResults (  
[vTargetMail],  
[vTargetMail DT],  
6,  
'Bike Buyer',  
1,  
0.5  
)  
```  
  
 Resultados do exemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Teste|Medida|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|v Target Mail DT|Bike Buyer|1|0|1638|Classificação|True Positivo|605|  
|v Target Mail DT|Bike Buyer|1|0|1638|Classificação|False Positivo|177|  
|v Target Mail DT|Bike Buyer|1|0|1638|Classificação|True Negativo|501|  
|v Target Mail DT|Bike Buyer|1|0|1638|Classificação|False Negativo|355|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilidade|Pontuação de log|-0.598454638753028|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilidade|Comparação de Precisão|0.0936717116894395|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilidade|Erro de Raiz Quadrada Média|0.361630800104946|  
  
## <a name="requirements"></a>Requisitos  
 A validação cruzada está disponível somente no [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services – mineração de dados&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
