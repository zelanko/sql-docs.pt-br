---
title: "SystemGetCrossValidationResults (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SystemGetCrossValidationResults
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
ms.assetid: f70c3337-c930-434a-b278-caf1ef0c3b3b
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 499e62070cb0ec0fed8e814c926d915f7e69bbe3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="systemgetcrossvalidationresults-analysis-services---data-mining"></a>SystemGetCrossValidationResults (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Partições que a estrutura de mineração em um número especificado de seções cruzadas, treina um modelo para cada partição e, em seguida, retorna métricas de precisão para cada partição.  
  
> [!NOTE]  
>  Esse procedimento armazenado não pode ser usado para fazer validação cruzada de modelos de clustering ou modelos criados usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo MTS ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] o algoritmo MSC. Para validação cruzada de modelos de clustering, você pode usar o procedimento armazenado separado, [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SystemGetCrossValidationResults(  
<mining structure>  
[, <mining model list>]  
,<fold count>  
,<max cases>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *estrutura de mineração*  
 Nome de uma estrutura de mineração no banco de dados atual.  
  
 (obrigatório)  
  
 *lista do modelo de mineração*  
 Lista separada por vírgulas de modelos de mineração para validar.  
  
 Se um nome de modelo contiver caracteres que não são válidos no nome de um identificador, o nome deverá ser colocado entre parênteses.  
  
 Se uma lista de modelos de mineração não for especificada, a validação cruzada será executada em todos os modelos de clustering associados com a estrutura especificada e que contenha um atributo previsível.  
  
> [!NOTE]  
>  Para validação cruzada de modelos de clustering, você deve usar um procedimento armazenado separado, [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
 (opcional)  
  
 *número de partições*  
 Inteiro que especifica o número de partições nas quais separar o conjunto de dados. O valor mínimo é 2. O número máximo de dobras é **maximum integer** ou o número de casos, o que for inferior.  
  
 Cada partição conterá este número de casos, aproximadamente: *máximo de casos*/*contagem de dobras*.  
  
 Não há valor padrão.  
  
> [!NOTE]  
>  O número de dobras afeta grandemente o tempo necessário para realizar a validação cruzada. Se você selecionar um número que seja muito alto, a consulta poderá ser executada por muito tempo e, em alguns casos, o servidor poderá ficar sem-resposta ou expirar.  
  
 (obrigatório)  
  
 *máximo de casos*  
 Inteiro que especifica o número máximo de casos que podem ser testados em todas as dobras.  
  
 Um valor de 0 indica que serão usadas todas as caixas na fonte de dados.  
  
 Se for especificado um valor maior que o de casos reais no conjunto de dados, todos os casos serão da fonte de dados serão usados.  
  
 Não há valor padrão.  
  
 (obrigatório)  
  
 *atributo de destino*  
 Cadeia de caracteres que contém o nome do atributo previsível. Um atributo previsível pode ser uma coluna, coluna de tabela aninhada ou coluna de chave de tabela aninhada de um modelo de mineração.  
  
> [!NOTE]  
>  A existência do atributo de destino só é validada no tempo de execução.  
  
 (obrigatório)  
  
 *estado de destino*  
 Fórmula que especifica o valor para prever. Se um valor de destino for especificado, as métricas serão coletadas somente para o valor especificado.  
  
 Se um valor não for especificado ou for **nulo**, as métrica serão computadas para o estado mais provável para cada previsão.  
  
 O padrão é **nulo**.  
  
 Um erro é gerado durante a validação se o valor especificado não for válido para o atributo especificado ou se a fórmula não for o tipo correto para o atributo especificado.  
  
 (opcional)  
  
 *limite*  *de destino*  
 **Double** maior que 0 e menor que 1. Indica a pontuação de probabilidade mínima que deve ser obtida para a previsão do estado de destino especificado ser contado como correto.  
  
 Uma previsão que tem uma probabilidade menor ou igual a este valor é considerada incorreta.  
  
 Se nenhum valor for especificado ou for **nulo**, o estado mais provável será usado, independentemente de sua pontuação de probabilidade.  
  
 O padrão é **nulo**.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]não gerará um erro se você definir *limiar de estado* como 0.0, mas você nunca deve usar esse valor. Na realidade, um limite de 0.0 significa que as previsões com uma probabilidade de 0 por cento foram contadas como corretas.  
  
 (opcional)  
  
 *test list*  
 Uma cadeia de caracteres que especifica opções de teste.  
  
 **Observação** : esse parâmetro é reservado para uso futuro.  
  
 (opcional)  
  
## <a name="return-type"></a>Tipo de retorno  
 O conjunto de linhas que é retornado contém pontuações para cada partição em cada modelo.  
  
 A tabela a seguir descreve as colunas no conjunto de linhas.  
  
|Nome da coluna|Description|  
|-----------------|-----------------|  
|ModelName|O nome do modelo que foi testado.|  
|AttributeName|O nome da coluna previsível.|  
|AttributeState|Um valor de destino especificado na coluna previsível. Se este valor for **nulo**, a previsão mais provável foi usada.<br /><br /> Se esta coluna contiver um valor, a precisão do modelo será avaliada com relação a esse valor somente.|  
|PartitionIndex|Um índice de base 1 que identifica a qual partição os resultados se aplicam.|  
|PartitionSize|Um inteiro que indica quantos casos foram incluídos em cada partição.|  
|Teste|Categoria do teste que foi executado. Para obter uma descrição das categorias e dos testes incluídos em cada categoria, consulte [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Measure|Nome da medida retornada pelo teste. Medidas para cada modelo dependem do tipo do valor previsível. Para obter uma definição de cada medida, consulte [Validação cruzada &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Para obter uma lista de medidas retornadas para cada tipo previsível, consulte [Medidas no relatório de validação cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Valor|O valor da medida de teste especificada.|  
  
## <a name="remarks"></a>Remarks  
 Para retornar métricas de precisão para o conjunto de dados completo, use [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
 Se o modelo de mineração já tiver sido dividido em dobras, você poderá ignorar o processamento e retornar somente os resultados da validação cruzada usando [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra como particionar uma estrutura de mineração para uma validação cruzada em três dobras e, em seguida, testar dois modelos de mineração associados com a estrutura de mineração, `[v Target Mail]`.  
  
 A linha três do código lista os modelos de mineração que você deseja testar. Se você não especificar a lista, todos os modelos que não forem de clustering associados à estrutura serão usados. A linha quatro do código especifica o número de partições. Como nenhum valor foi especificado para *máximo de casos*, todos os casos na estrutura de dados serão usados e distribuídos uniformemente nas partições.  
  
 A linha cinco especifica o atributo previsível, Comprador de Bicicleta, e a linha seis especifica o valor para prever, 1 ("sim, comprará").  
  
 O valor NULL da linha sete indica que não há barra de probabilidade mínima a ser correspondida. Então, a primeira previsão com uma probabilidade diferente de zero será usada na avaliação da precisão.  
  
```  
CALL SystemGetCrossValidationResults(  
[v Target Mail],  
[Target Mail DT], [Target Mail NB],  
2,  
'Bike Buyer',  
1,  
NULL  
)  
```  
  
 Resultados do exemplo:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Teste|Medida|Valor|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Target Mail DT|Bike Buyer|1|1|500|Classificação|True Positivo|144|  
|Target Mail DT|Bike Buyer|1|1|500|Classificação|False Positivo|105|  
|Target Mail DT|Bike Buyer|1|1|500|Classificação|True Negativo|186|  
|Target Mail DT|Bike Buyer|1|1|500|Classificação|False Negativo|65|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilidade|Pontuação de log|-0.619042807138345|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilidade|Comparação de Precisão|0.0740963734002671|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilidade|Erro de Raiz Quadrada Média|0.346946279977653|  
|Target Mail DT|Bike Buyer|1|2|500|Classificação|True Positivo|162|  
|Target Mail DT|Bike Buyer|1|2|500|Classificação|False Positivo|86|  
|Target Mail DT|Bike Buyer|1|2|500|Classificação|True Negativo|165|  
|Target Mail DT|Bike Buyer|1|2|500|Classificação|False Negativo|87|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilidade|Pontuação de log|-0.654117781086519|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilidade|Comparação de Precisão|0.038997399132084|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilidade|Erro de Raiz Quadrada Média|0.342721344892651|  
  
## <a name="requirements"></a>Requisitos  
 A validação cruzada está disponível somente no [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [SystemGetCrossValidationResults](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40; Analysis Services – mineração de dados &#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40; Analysis Services – mineração de dados &#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
