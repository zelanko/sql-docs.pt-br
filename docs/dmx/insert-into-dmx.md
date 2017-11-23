---
title: INSERIR (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INSERT INTO
- INSERT
- INSERT_INTO
dev_langs: DMX
helpviewer_keywords:
- SKIP (DMX)
- mapped model columns element
- source data query element
- <mapped model columns> element
- <source data query> element
- INSERT INTO statement
- mining models [Analysis Services], processing
- training mining models
- mining structures [DMX], processing
ms.assetid: 85eed207-396c-4a95-a74e-2acc1abc7e2c
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6effd75e67a69db182ddaf37388d377b644a17da
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Processa o objeto de mineração de dados especificado. Para obter mais informações sobre o processamento de modelos de mineração e estruturas de mineração, consulte [processamento requisitos e considerações sobre &#40; mineração de dados &#41;](../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Se uma estrutura de mineração for especificada, a instrução processará a estrutura de mineração e todos seus modelos de mineração associados. Se o modelo de mineração for especificado, a instrução processará apenas o modelo de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argumentos  
 *modelo*  
 Identificador de modelo.  
  
 *estrutura*  
 Identificador de estrutura.  
  
 *colunas de modelo mapeado*  
 Lista separada por vírgula de identificadores de coluna e identificadores aninhados.  
  
 *consulta de fonte de dados*  
 Consulta da fonte no formato definido pelo provedor.  
  
## <a name="remarks"></a>Comentários  
 Se você não especificar **modelo de MINERAÇÃO** ou **estrutura de MINERAÇÃO**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] procura o tipo de objeto com base no nome e, em seguida, processa o objeto correto. Se o servidor contiver uma estrutura de mineração e um modelo de mineração com nomes idênticos, um erro será retornado.  
  
 Usando o segundo formulário de sintaxe, INSERT INTO*\<objeto >*. COLUMN_VALUES, você pode inserir dados diretamente nas colunas de modelo, sem treinar o modelo. Esse método fornece dados de coluna para o modelo de forma concisa, ordenada, que é útil quando se trabalha com conjuntos de dados contendo hierarquias ou colunas ordenadas.  
  
 Se você usar **INSERT INTO** com um modelo de mineração ou uma estrutura de mineração e deixe desativar o \<mapear colunas de modelo > e \<consulta de fonte de dados > argumentos, a instrução se comporta como **ProcessDefault**, usando associações já existentes. Se não houver associações, a instrução retornará um erro. Para obter mais informações sobre **ProcessDefault**, consulte [opções de processamento e as configurações de &#40; Analysis Services &#41; ](../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md). O exemplo a seguir mostra a sintaxe:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Se você especificar **modelo de MINERAÇÃO** e fornecer colunas mapeadas e uma consulta de fonte de dados, o modelo e estrutura associada é processado.  
  
 A tabela a seguir fornece uma descrição do resultado de diferentes formas de instruções, dependendo do estado dos objetos.  
  
|de|Estado de objetos|Resultado|  
|---------------|----------------------|------------|  
|INSERT INTO MINING MODEL*\<modelo >*|A estrutura de mineração é processada.|O modelo de mineração é processado.|  
||A estrutura de mineração é não processada.|O modelo de mineração e a estrutura de mineração são processadas.|  
||A estrutura de mineração contém modelos de mineração adicionais.|Falha no processo. É preciso reprocessar a estrutura e os modelos de mineração associados.|  
|INSERT INTO MINING STRUCTURE*\<estrutura >*|A estrutura de mineração é processada ou não processada.|A estrutura de mineração e os modelos de mineração associados são processados.|  
|INSERT INTO MINING MODEL*\<modelo >* que contém uma consulta de origem<br /><br /> ou<br /><br /> INSERT INTO MINING STRUCTURE*\<estrutura >* que contém uma consulta de origem|A estrutura ou o modelo já encerram um conteúdo.|Falha no processo. Você deve limpar os objetos antes de executar essa operação, usando [Excluir &#40; DMX &#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Colunas de modelo mapeado  
 Usando o \<mapear colunas de modelo > elemento, você pode mapear as colunas da fonte de dados para as colunas no modelo de mineração. O \<mapear colunas de modelo > elemento tem o seguinte formato:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Usando **ignorar**, você pode excluir determinadas colunas que devem existir na consulta de fonte, mas que não existem no modelo de mineração. SKIP é útil quando você não tem controle sobre as colunas que estão incluídas no conjunto de linhas de entrada. Se você estiver escrevendo sua própria OPENQUERY, a prática recomendada é omitir a coluna da lista de colunas SELECT em vez de usar SKIP.  
  
 SKIP também é útil quando uma coluna do conjunto de linhas de entrada é necessária para executar uma junção, mas a coluna não é usada pela estrutura de mineração. Um exemplo típico disso é uma estrutura de mineração e modelo de mineração que contêm uma tabela aninhada. O conjunto de linhas de entrada desta estrutura terá uma coluna de chave estrangeira usada para criar um conjunto de linhas hierárquico usando a cláusula SHAPE, mas a coluna de chave estrangeira quase nunca é usada no modelo.  
  
 A sintaxe de SKIP requer que você insira SKIP na posição da coluna individual no conjunto de linhas de entrada que não tem nenhuma coluna de estrutura de mineração correspondente. Por exemplo, na tabela aninhada a seguir, OrderNumber deve ser selecionado na cláusula APPEND para que possa ser usado na cláusula RELATE para especificar a junção. No entanto, você não precisa inserir os dados de OrderNumber na tabela aninhada na estrutura de mineração. Portanto o exemplo usa a palavra-chave SKIP em vez de OrderNumber no argumento INSERT INTO.  
  
## <a name="source-data-query"></a>Consulta de dados de origem  
 O \<consulta de fonte de dados > elemento pode incluir os seguintes tipos de fonte de dados:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **FORMA**  
  
-   Qualquer consulta [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que retorne um conjunto de linhas  
  
 Para obter mais informações sobre tipos de fonte de dados, consulte [&#60; consulta de fonte de dados &#62;](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Exemplo básico  
 O exemplo a seguir usa **OPENQUERY** para treinar um modelo Naive Bayes com base em dados de endereçamento de destino no [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] banco de dados.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Exemplo de tabela aninhada  
 O exemplo a seguir usa **forma** para treinar um modelo de mineração de associação que contém uma tabela aninhada. Observe que a primeira linha contém **ignorar** em vez disso, OrderNumber que é necessário o **SHAPE_APPEND** instrução, mas não é usada no modelo de mineração.  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
