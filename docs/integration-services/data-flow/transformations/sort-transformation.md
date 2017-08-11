---
title: "Transformação classificação | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sorttrans.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bb0f93339416c071177fd532847b584ab2043e84
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="sort-transformation"></a>Transformação Classificação
  A transformação Classificação ordena os dados de entrada de modo crescente ou decrescente e os copia na saída da transformação. Você pode aplicar várias classificações a uma entrada. Cada classificação é identificada por um numeral que determina a ordem de classificação. A coluna com o número mais baixo é classificada primeiro, a com o segundo número mais baixo é classificada em seguida e assim por diante. Por exemplo, se uma coluna denominada **CountryRegion** tiver uma ordem de classificação 1 e uma coluna denominada **City** tiver uma ordem de classificação 2, a saída será ordenada por país/região e depois por cidade. Um número positivo indica que a classificação está aumentando, e um negativo que está diminuindo. As colunas que não forem classificadas terão a ordem de classificação 0. As colunas que não forem selecionadas para classificação serão automaticamente copiadas para a saída de transformação junto com as colunas classificadas.  
  
 A transformação Classificação inclui um conjunto de opções de comparação para definir como a transformação controla os dados de cadeia de caracteres em uma coluna. Para obter mais informações, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
> [!NOTE]  
>  A transformação Classificação não ordena os GUIDs na mesma ordem como a cláusula ORDER BY faz em Transact-SQL. Enquanto a transformação Classificação ordena os GUIDs que iniciam com 0-9 antes dos GUIDs que iniciam com A-F, a cláusula ORDER BY, como implementado no [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], faz a classificação de modo diferente. Para obter mais informações, consulte [Cláusula ORDER BY &#40;Transact-SQL&#41;](../../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
 A transformação Classificação também pode remover linhas duplicadas como parte de sua classificação. Linhas duplicadas são linhas com os mesmos valores da chave de classificação. O valor da chave de classificação é gerado com base nas opções de comparação da cadeia de caracteres que estiverem sendo usadas. Isto significa que cadeias de caracteres literais diferentes podem ter os mesmos valores da chave de classificação. A transformação identifica como duplicidade as linhas nas colunas de entrada que têm valores diferentes porém a mesma chave de classificação.  
  
 A transformação Classificação inclui a propriedade personalizada **MaximumThreads** que pode ser atualizada por uma expressão de propriedade quando o pacote for carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada e uma saída. Ela não oferece suporte a saídas de erro.  
  
## <a name="configuration-of-the-sort-transformation"></a>Configuração da transformação Classificação  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou programaticamente.  
  
 Para obter informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Classificação** , consulte [Sort Transformation Editor](../../../integration-services/data-flow/transformations/sort-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter mais informações sobre como definir as propriedades do componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Exemplo, [SortDeDuplicateDelimitedString Custom SSIS Component](http://go.microsoft.com/fwlink/?LinkId=220821), em codeplex.com.  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
