---
title: Transformação Classificação | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
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
manager: craigg
ms.openlocfilehash: a20feb9d15a24ea417a715816e3b437e13d0ca2c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir as propriedades do componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Exemplo, [SortDeDuplicateDelimitedString Custom SSIS Component](http://go.microsoft.com/fwlink/?LinkId=220821), em codeplex.com.  
  
## <a name="sort-transformation-editor"></a>Editor de Transformação Classificação
  Use a caixa de diálogo **Editor de Transformação Classificação** para selecionar as colunas a classificar, definir a ordem de classificação e especificar se as duplicatas devem ser removidas.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Usando as caixas de seleção, especifique as colunas a classificar.  
  
 **Nome**  
 Visualize o nome de cada coluna de entrada disponível.  
  
 **Passagem**  
 Indique se a coluna deve ser incluída na saída classificada.  
  
 **Coluna de Entrada**  
 Selecione colunas para cada linha na lista de colunas de entrada disponíveis. As seleções se refletem naquelas da caixa de seleção da tabela **Colunas de Entrada Disponíveis** .  
  
 **Alias de Saída**  
 Digite um alias para cada coluna de saída. O padrão é o nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Tipo de Classificação**  
 Indique se a classificação deve ser feita em ordem ascendente ou descendente.  
  
 **Sort Order**  
 Indique a ordem na qual classificar as colunas. Deve ser definido manualmente para cada coluna.  
  
 **Sinalizadores de Comparação**  
 Para obter mais informações sobre as opções de comparação de cadeias de caracteres, consulte [Comparando dados de cadeia de caracteres](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Remover linhas com valores de classificação duplicados**  
 Indique se a transformação deve copiar as linhas duplicadas para a saída ou criar uma única entrada para todas as duplicatas, seguindo as opções de comparação de cadeia de caracteres especificadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
