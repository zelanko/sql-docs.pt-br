---
title: Conjuntos de dados de treinamento e teste | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- testing mining models
- holdout [data mining]
- testing data mining models
- accuracy testing [data mining]
ms.assetid: 5798fa48-ef3c-4e97-a17c-38274970fccd
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4e050a59da542041b9ce825f573625bdb6afc289
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520318"
---
# <a name="training-and-testing-data-sets"></a>Conjuntos de dados de teste e treinamento
  A separação de dados em conjuntos de teste e treinamento é uma parte importante da avaliação de modelos de mineração de dados. Normalmente, quando você separa um conjunto de dados em um conjunto de treinamentos e um conjunto de testes, a maior parte dos dados é usada para treinamento e uma parte menor dos dados é usada para teste. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] faz a amostra aleatória dos dados para ajudar a garantir que as partições de teste e de treinamento são similares. Usando dados semelhantes para treinamento e teste, você pode minimizar os efeitos das discrepâncias de dados e entender melhor as características do modelo.  
  
 Depois que um modelo for processado usando o conjunto de treinamentos, você testa o modelo fazendo previsões contra o conjunto de testes. Como os dados no conjunto de teste já contêm valores conhecidos para o atributo que você deseja prever, é fácil determinar se a precisão das previsões do modelo está correta.  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>Criando conjuntos de dados de teste e treinamento para estruturas de mineração de dados  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você separa o conjunto de dados original no nível da estrutura de mineração. As informações sobre o tamanho dos conjuntos de dados de teste e treinamento, e qual linha corresponde a qual conjunto são armazenados com a estrutura e todos os modelos baseados nessa estrutura podem usar os conjuntos para treinamento e teste.  
  
 Você pode definir um conjunto de dados de teste em uma estrutura de mineração dos seguintes modos:  
  
-   Usando o Assistente de Mineração de Dados para dividir uma estrutura de mineração quando você a cria.  
  
-   Modificando as propriedades de estrutura na guia **Estrutura de Mineração** do Designer de Mineração de Dados.  
  
-   Criando e modificando as estruturas programaticamente usando os Objetos de Gerenciamento de Análise (AMO) ou a linguagem de definição de dados DDL.  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>Usando o Assistente de Mineração de Dados para dividir uma estrutura de mineração  
 Por padrão, depois de definir as fontes de dados para uma estrutura de mineração, a Assistente de Mineração de Dados dividirá os dados em dois conjuntos: um com 70% dos dados de origem, para treinar o modelo, e um com 30% para testar o modelo. Esse padrão foi escolhido porque a proporção de 70-30 é geralmente usada na mineração de dados, mas com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode alterar essa proporção para adequar suas exigências.  
  
 Você também pode configurar o assistente para definir um número máximo de casos de treinamento de casos ou você pode combinar os limites para limitar uma porcentagem máxima de casos até um número máximo de casos especificados. Quando você especifica uma porcentagem máxima de casos e um número máximo de casos, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa o menor dos dois limites como o tamanho do conjunto de teste. Por exemplo, se você especificar uma validação de 30% para testar casos e o número máximo de casos de teste como 1.000, o tamanho do conjunto de teste nunca excederá 1.000 casos. Isso pode ser útil se quiser garantir que o tamanho do seu conjunto de teste se mantenha consistente mesmo que mais dados de treinamento sejam adicionados ao modelo.  
  
 Se você usar a mesma exibição de fonte de dados para estruturas de mineração diferentes e quiser garantir que os dados sejam divididos aproximadamente da mesma forma para todas as estruturas de mineração e seus modelos, você deve especificar a semente usada para inicializar a amostragem aleatória. Quando você especificar um valor para `HoldoutSeed`, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará esse valor para iniciar a amostragem. Caso contrário, a amostragem usa um algoritmo de hash no nome da estrutura de mineração para criar o valor de semente.  
  
> [!NOTE]  
>  Se você criar uma cópia da estrutura de mineração usando as instruções `EXPORT` e `IMPORT`, a nova estrutura de mineração terá os mesmos conjuntos de dados de treinamento e teste, porque o processo de exportação cria uma nova ID, mas usa o mesmo nome. No entanto, se duas estruturas de mineração usam a mesma fonte de dados subjacente, mas têm nomes diferentes, os conjuntos criados para cada estrutura de mineração serão diferentes.  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>Modificando propriedades de estrutura para criar um conjunto de dados de teste  
 Se você criar e processar uma estrutura de mineração e posteriormente decidir que deseja definir separadamente um conjunto de dados de teste, poderá modificar as propriedades da estrutura de mineração. Para alterar a maneira que os dados são particionados, edite as seguintes propriedades:  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`HoldoutMaxCases`|Especifica o número máximo de casos a serem incluídos no conjunto de teste.|  
|`HoldoutMaxPercent`|Especifica o número de casos a serem incluídos no conjunto de teste como uma porcentagem do conjunto de dados completo. Para não ter nenhum conjunto de dados, especifique 0.|  
|`HoldoutSeed`|Especifica um valor inteiro a ser usado como semente ao selecionar dados aleatoriamente para as partições. Esse valor não afeta o número de casos no conjunto de treinamento; ao contrário, ele garante que a partição pode ser repetida.|  
  
 Se você adicionar ou alterar um conjunto de dados de teste a uma estrutura existente, deverá reprocessar a estrutura e todos os modelos associados. Além disso, como dividir os dados de origem faz o modelo ser treinado em um subconjunto diferente de dados, você deve ver resultados diferentes a partir do seu modelo.  
  
### <a name="specifying-holdout-programmatically"></a>Especificando controle programaticamente  
 Você pode definir conjuntos de dados de teste e treinamento em uma estrutura de mineração usando instruções DMX, AMO ou XML DDL. A instrução ALTER MINING STRUCTURE não oferece suporte ao uso dos parâmetros de controle.  
  
-   **DMX** Na linguagem DMX (extensões DMX), a instrução CREATE MINING STRUCTURE foi ampliada para incluir uma cláusula WITH HOLDOUT.  
  
-   **ASSL** Você pode criar uma nova estruturas de mineração ou adicionar um conjunto de dados de teste a uma estrutura de mineração existente, usando a ASSL ( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Scripting Language).  
  
-   **AMO** Você também pode exibir e modificar os conjuntos de dados de controle usando AMO.  
  
 Você pode exibir informações sobre os conjuntos de dados de controle em uma estrutura de mineração existente consultando o conjunto de linhas do esquema de mineração de dados. Você pode fazer isso através de uma chamada DISCOVER ROWSET ou usando uma consulta DMX.  
  
## <a name="retrieving-information-about-holdout-data"></a>Recuperando informações sobre dados de controle  
 Por padrão, todas as informações sobre os conjuntos de dados de treinamento e de teste estão armazenadas em cache, assim você pode usar os dados para treinamento e depois testar os novos modelos. Você também pode definir os filtros a serem aplicados aos dados de controle armazenados em cache, assim pode avaliar o modelo nos subconjuntos de dados.  
  
 O modo como os casos são divididos em conjuntos de dados de treinamento e teste depende de como você configura o controle e dos dados que você fornece. Se você quiser determinar o número de casos usados para treinamento ou teste, ou se você quer localizar detalhes adicionais sobre os casos incluídos nos conjuntos de treinamento e teste, você pode consultar a estrutura de modelo criando uma consulta DMX. Por exemplo, a consulta a seguir retorna os casos usados no conjunto de treinamento do modelo.  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 Para recuperar somente os casos de teste e filtrar adicionalmente os casos de teste em uma das colunas na estrutura de mineração, use a seguinte sintaxe:  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>Limitações no uso de dados de controle  
  
-   Para usar o controle, a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> da estrutura de mineração deve ser definida como o valor padrão, `KeepTrainingCases`. Se você alterar a propriedade `CacheMode` para `ClearAfterProcessing` e, em seguida, reprocessar a estrutura de mineração, a partição será perdida.  
  
-   Você não pode remover dados de um modelo de série temporal; portanto, você não pode separar os dados de origem em conjuntos de treinamento e teste. Se você começar a criar uma estrutura de mineração e modelo e escolher o algoritmo MTS ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series), a opção de criar um conjunto de dados de controle será desabilitada. O uso de dados de controle também será desabilitado se a estrutura de mineração contiver uma coluna KEY TIME no caso ou no nível de tabela aninhada.  
  
-   É possível configurar inadvertidamente os conjuntos de dados de controle de modo que o conjunto de dados inteiro seja usado em testes e nenhum dado permanecer para usar em treinamento. Porém, se você fizer assim, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gerará um erro de forma que você possa corrigir o problema. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também avisa você quando a estrutura é processada se mais de 50% dos dados tiverem sido validados para teste.  
  
-   Na maioria dos casos, o valor de validação padrão de 30 fornece um bom equilíbrio entre os dados de treinamento e teste. Não há uma maneira simples de determinar o tamanho necessário do conjunto de dados para fornecer treinamento suficiente, nem o quão esparso o conjunto de treinamentos pode ser e, conseguir, ainda, evitar o superajuste. Porém, depois que você criar um modelo, pode usar validação cruzada para avaliar o conjunto de dados em relação a um modelo específico.  
  
-   Além das propriedades listadas na tabela anterior, uma propriedade somente leitura `HoldoutActualSize` é fornecida no AMO e XML DDL. No entanto, como o tamanho real de uma partição não pode ser determinado precisamente até que a estrutura tenha sido processada, você deve verificar se o modelo foi processado antes de recuperar o valor da propriedade `HoldoutActualSize`.  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
|Tópicos|Links|  
|------------|-----------|  
|Descreve como os filtros em um modelo interagem com conjuntos de dados de treinamento e teste.|[Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-models-analysis-services-data-mining.md)|  
|Descreve como o uso de dados de treinamento e teste afeta a validação cruzada.|[Validação cruzada &#40;Analysis Services – Data Mining&#41;](cross-validation-analysis-services-data-mining.md)|  
|Fornece informações sobre as interfaces programáticas para funcionar com conjuntos de treinamento e teste em uma estrutura de mineração.|[Conceitos de AMO e modelo de objeto](https://docs.microsoft.com/bi-reference/amo/amo-concepts-and-object-model)<br /><br /> [Elemento MiningStructure &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/objects/miningstructure-element-assl)|  
|Fornece sintaxe de DMX para criar conjuntos de controle.|[CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)|  
|Recuperar informações sobre casos nos conjuntos de treinamento e teste.|[Conjuntos de linhas de esquema de mineração de dados](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)<br /><br /> [Consultando os conjuntos de linhas do esquema de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de mineração de dados](data-mining-tools.md)   
 [Conceitos de mineração de dados](data-mining-concepts.md)   
 [Soluções de mineração de dados](data-mining-solutions.md)   
 [Teste e validação &#40;Mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
  
