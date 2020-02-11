---
title: INSERIR EM (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 210ab8c5750fdcb38bcbca324d77eecd926042d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892721"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Processa o objeto de mineração de dados especificado. Para obter mais informações sobre como processar modelos de mineração e estruturas de mineração, consulte [requisitos e considerações de processamento &#40;&#41;de mineração de dados ](https://docs.microsoft.com/analysis-services/data-mining/processing-requirements-and-considerations-data-mining).  
  
 Se uma estrutura de mineração for especificada, a instrução processará a estrutura de mineração e todos seus modelos de mineração associados. Se o modelo de mineração for especificado, a instrução processará apenas o modelo de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argumentos  
 *modelo*  
 Identificador de modelo.  
  
 *estruturá*  
 Identificador de estrutura.  
  
 *colunas de modelo mapeado*  
 Lista separada por vírgula de identificadores de coluna e identificadores aninhados.  
  
 *consulta de dados de origem*  
 Consulta da fonte no formato definido pelo provedor.  
  
## <a name="remarks"></a>Comentários  
 Se você não especificar o **modelo de mineração** ou a estrutura [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de **mineração**, o procurará o tipo de objeto com base no nome e processará o objeto correto. Se o servidor contiver uma estrutura de mineração e um modelo de mineração com nomes idênticos, um erro será retornado.  
  
 Usando o segundo formulário de sintaxe, insira no*\<objeto>*. COLUMN_VALUES, você pode inserir dados diretamente nas colunas de modelo sem treinar o modelo. Esse método fornece dados de coluna para o modelo de forma concisa, ordenada, que é útil quando se trabalha com conjuntos de dados contendo hierarquias ou colunas ordenadas.  
  
 Se você usar **inserir em** com um modelo de mineração ou uma estrutura de mineração, e deixar \<de fora as colunas de \<modelo mapeado> e> argumentos de consulta de dados de origem, a instrução se comportará como **ProcessDefault**, usando associações que já existem. Se não houver associações, a instrução retornará um erro. Para obter mais informações sobre **ProcessDefault**, consulte [Opções de processamento e configurações &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services). O exemplo a seguir mostra a sintaxe:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Se você especificar o **modelo de mineração** e fornecer colunas mapeadas e uma consulta de dados de origem, o modelo e a estrutura associada serão processados.  
  
 A tabela a seguir fornece uma descrição do resultado de diferentes formas de instruções, dependendo do estado dos objetos.  
  
|de|Estado de objetos|Result|  
|---------------|----------------------|------------|  
|Inserir no modelo de*\<modelo de mineração>*|A estrutura de mineração é processada.|O modelo de mineração é processado.|  
||A estrutura de mineração é não processada.|O modelo de mineração e a estrutura de mineração são processadas.|  
||A estrutura de mineração contém modelos de mineração adicionais.|Falha no processo. É preciso reprocessar a estrutura e os modelos de mineração associados.|  
|Inserir na estrutura da*\<estrutura de mineração>*|A estrutura de mineração é processada ou não processada.|A estrutura de mineração e os modelos de mineração associados são processados.|  
|Inserir no*\<modelo* modelo de mineração>que contém uma consulta de origem<br /><br /> ou<br /><br /> Inserir em*\<estrutura* de estrutura de mineração>que contém uma consulta de origem|A estrutura ou o modelo já encerram um conteúdo.|Falha no processo. Você deve limpar os objetos antes de executar essa operação, usando [excluir &#40;DMX&#41;](../dmx/delete-dmx.md).|  
  
## <a name="mapped-model-columns"></a>Colunas de modelo mapeado  
 Usando o \<elemento> de colunas de modelo mapeado, você pode mapear as colunas da fonte de dados para as colunas em seu modelo de mineração. O \<elemento de> de colunas de modelo mapeado tem a seguinte forma:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Ao usar **Skip**, você pode excluir determinadas colunas que devem existir na consulta de origem, mas que não existem no modelo de mineração. SKIP é útil quando você não tem controle sobre as colunas que estão incluídas no conjunto de linhas de entrada. Se você estiver escrevendo sua própria OPENQUERY, a prática recomendada é omitir a coluna da lista de colunas SELECT em vez de usar SKIP.  
  
 SKIP também é útil quando uma coluna do conjunto de linhas de entrada é necessária para executar uma junção, mas a coluna não é usada pela estrutura de mineração. Um exemplo típico disso é uma estrutura de mineração e modelo de mineração que contêm uma tabela aninhada. O conjunto de linhas de entrada desta estrutura terá uma coluna de chave estrangeira usada para criar um conjunto de linhas hierárquico usando a cláusula SHAPE, mas a coluna de chave estrangeira quase nunca é usada no modelo.  
  
 A sintaxe de SKIP requer que você insira SKIP na posição da coluna individual no conjunto de linhas de entrada que não tem nenhuma coluna de estrutura de mineração correspondente. Por exemplo, na tabela aninhada a seguir, OrderNumber deve ser selecionado na cláusula APPEND para que possa ser usado na cláusula RELATE para especificar a junção. No entanto, você não precisa inserir os dados de OrderNumber na tabela aninhada na estrutura de mineração. Portanto o exemplo usa a palavra-chave SKIP em vez de OrderNumber no argumento INSERT INTO.  
  
## <a name="source-data-query"></a>Consulta de dados de origem  
 O \<elemento> de consulta de dados de origem pode incluir os seguintes tipos de fonte de dados:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **LA**  
  
-   Qualquer consulta [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que retorne um conjunto de linhas  
  
 Para obter mais informações sobre tipos de fonte de dados, consulte [&#60;&#62;de consulta de dados de origem ](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Exemplo básico  
 O exemplo a seguir usa **OPENQUERY** para treinar um modelo Naive Bayes com base nos dados de endereçamento direcionados no banco de [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] dado.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Exemplo de tabela aninhada  
 O exemplo a seguir usa a **forma** para treinar um modelo de mineração de associação que contém uma tabela aninhada. Observe que a primeira linha contém **Skip** em vez de OrderNumber, que é necessário na instrução **SHAPE_APPEND** , mas não é usado no modelo de mineração.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
