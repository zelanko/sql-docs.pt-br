---
title: Referência de propriedades de atributo de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- properties [Analysis Services], attributes
- attributes [Analysis Services], properties
ms.assetid: 7f83d1cb-4732-424f-adc5-2449c1dd1008
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cc66df28276802d7d397e498ceb1a22abdedb80e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006435"
---
# <a name="dimension-attribute-properties-reference"></a>Referência de propriedades de atributo de dimensão
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], existem muitas propriedades que determinam como funcionam as dimensões e os atributos da dimensão. A tabela a seguir lista e descreve cada uma dessas propriedades de atributo.  
  
|Propriedade|Description|  
|--------------|-----------------|  
|`AttributeHierarchyDisplayFolder`|Identifica a pasta na qual deve ser exibida a hierarquia de atributo associada aos usuários finais.|  
|`AttributeHierarchyEnabled`|Determina se uma hierarquia de atributo é gerada pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o atributo. Se a hierarquia de atributo não for habilitada, o atributo não poderá ser usado em uma hierarquia definida pelo usuário e a hierarquia de atributo não poderá ser consultada nas instruções de linguagem MDX.|  
|`AttributeHierarchyOptimizedState`|Determina o nível de otimização aplicado à hierarquia de atributo. Por padrão, uma hierarquia de atributo é `FullyOptimized`, o que significa que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria índices para a hierarquia de atributo para aprimorar o desempenho de consulta. A outra opção, `NotOptimized`, significa que nenhum índice é criado para a hierarquia de atributo. Usando `NotOptimized` será útil se a hierarquia de atributo é usada para finalidades diferentes de consulta, pois nenhum índice adicional será criado para o atributo. Outros usos para uma hierarquia de atributo podem estar ajudando a ordenar outro atributo.|  
|`AttributeHierarchyOrdered`|Determina se a hierarquia de atributo associada está ordenada. O valor padrão é `True`. No entanto, se uma hierarquia de atributo não será usada para consultar, você pode poupar tempo de processamento, alterando o valor dessa propriedade como `False`.|  
|`AttributeHierarchyVisible`|Determina se a hierarquia de atributo é visível a aplicativos cliente. O valor padrão é `True`. No entanto, se uma hierarquia de atributo não será usada para consultar, você pode poupar tempo de processamento, alterando o valor dessa propriedade como `False`.|  
|`CustomRollupColumn`|Especifica a coluna que define uma fórmula de rollup personalizado.|  
|`CustomRollupPropertiesColumn`|Especifica a coluna que contém as propriedades de uma fórmula de rollup personalizado.|  
|`DefaultMember`|Especifica uma expressão de linguagem MDX que define a medida padrão para o atributo.|  
|`Description`|Contém a descrição do atributo.|  
|`DiscretizationBucketCount`|Contém o número de recipientes nos quais são diferenciados.|  
|`DiscretizationMethod`|Define o método a ser usado para diferenciação.|  
|`EstimatedCount`|Especifica o número estimado de membros no atributo. Até a execução do Assistente de Design de Agregação, o valor padrão é zero. Você pode permitir que o assistente conte o número de registros ou digitar um valor estimado. Digite um valor manualmente se você souber o número de membros e quiser economizar o tempo necessário para consultar o banco de dados da conta. Se você estiver trabalhando com um subconjunto de testes de seus dados de produção, será possível usar as contagens dos dados de produção de forma que o design de agregação seja otimizado para os dados de produção em vez dos dados de teste.|  
|`GroupingBehavior`|Um valor definido pelo usuário que fornece uma dica para aplicativos cliente sobre como agrupar atributos.|  
|`ID`|Contém o identificador exclusivo (ID) da dimensão.|  
|`InstanceSelection`|Fornece uma dica para aplicativos cliente sobre como uma lista de itens deve ser exibida, com base no número esperado de itens na lista. As opções disponíveis são as seguintes:<br /><br /> **None** Nenhuma dica é fornecida ao aplicativo cliente. Este é o valor padrão.<br /><br /> **DropDown** O número de itens é pequeno o suficiente para ser exibido em uma lista suspensa.<br /><br /> **List** O número de itens é muito grande para uma **lista**suspensa, mas não requer filtragem.<br /><br /> **FilteredList** O número de itens é grande o suficiente para exigir que os usuários filtrem os itens a serem exibidos.<br /><br /> **MandatoryFilter** O número de itens é tão grande que a exibição deve sempre ser filtrada.|  
|`IsAggregatable`|Especifica se os valores dos membros de atributo podem ser agregados. O valor padrão é `True`, que significa que a hierarquia de atributo contém um nível (All). Se o valor dessa propriedade for `False`, a hierarquia de atributo não conterá um nível (All).|  
|`KeyColumns`|Contém a coluna ou as colunas que representam a chave para o atributo, que é a coluna na tabela relacional subjacente na exibição da fonte de dados à qual o atributo está associado. O valor dessa coluna para cada membro será exibido aos usuários a menos que um valor seja especificado para a propriedade `NameColumn`.|  
|`MemberNamesUnique`|Determina se nomes de membro na hierarquia de atributo devem ser exclusivos.|  
|`MembersWithData`|Usado por atributos pai para determinar se devem ou não exibir membros de dados para membros não folha no atributo pai. O valor da propriedade é usado apenas quando o valor da `Usage` propriedade está definida como pai. Isso significa que uma hierarquia pai-filho foi definida. As opções disponíveis são as seguintes:<br /><br /> **NonLeafDataHidden** Dados não folha estão ocultos.<br /><br /> **NonLeafDataVisible** Dados não folha estão visíveis.|  
|`MembersWithDataCaption`|Fornece uma cadeia de caracteres modelo usada por atributos pai para criar legendas para membros de dados gerados pelo sistema no atributo pai. O valor da propriedade é usado apenas quando o valor da `Usage` propriedade está definida como pai. Isso significa que uma hierarquia pai-filho foi definida.|  
|`Name`|Contém o nome amigável do atributo.|  
|`NameColumn`|Identifica a coluna que fornece o nome do atributo exibido aos usuários, em vez do valor na coluna de chave do atributo. Essa coluna será usada quando o valor da coluna de chave de um membro de atributo for secreto ou não for útil ao usuário, ou quando a coluna de chave for baseada em uma chave composta. A propriedade `NameColumn` não é usada em hierarquias pai-filho; em vez disso, a propriedade `NameColumn` para membros filho é usada como nomes de membro em uma hierarquia pai-filho.|  
|`NamingTemplate`|Define como os níveis construídos a partir do atributo pai são nomeados em uma hierarquia pai-filho. O valor da propriedade é usado apenas quando o valor da `Usage` propriedade está definida como pai. Isso significa que uma hierarquia pai-filho foi definida.|  
|`OrderBy`|Descreve como ordenar os membros contidos na hierarquia de atributo. O valor padrão é o nome, que especifica que a ordenação dos membros de atributo se baseia no valor da `NameColumn` propriedade, se houver. Caso contrário, os membros são ordenados pelo valor da coluna de chave. As opções disponíveis são as seguintes:<br /><br /> `NameColumn` Ordem pelo valor da `NameColumn` propriedade.<br /><br /> **Key** Ordem pelo valor da coluna de chave do membro de atributo.<br /><br /> **AttributeKey** Ordem pelo valor da chave de membro de um atributo especificado, que deve ter uma relação de atributo com o atributo.<br /><br /> **AttributeName** Ordem pelo valor do nome de membro de um atributo especificado, que deve ter uma relação de atributo com o atributo.|  
|`OrderByAttribute`|Identifica com qual atributo os membros da hierarquia de atributo são ordenados.|  
|`RootMemberIf`|Determina como os membros raiz ou superiores de uma hierarquia pai-filho são identificados. O valor da propriedade é usado apenas quando o valor da `Usage` propriedade está definida como pai. Isso significa que uma hierarquia pai-filho foi definida. O valor padrão é `ParentIsBlankSelfOrMissing`, que significa que somente membros que atendam a uma ou mais das condições descritas para `ParentIsBlank`, `ParentIsSelf`ou `ParentIsMissing` são tratados como membros raiz. Os seguintes valores também estão disponíveis:<br /><br /> `ParentIsBlank` Somente membros com um valor nulo, um zero ou uma cadeia de caracteres vazia na coluna de chave ou colunas são tratados como membros raiz.<br /><br /> `ParentIsSelf` Somente os membros com eles próprios como pais são tratados como membros raiz.<br /><br /> `ParentIsMissing` Somente membros com pais que não podem ser encontrados são tratados como membros raiz.|  
|`Type`|Contém o tipo do atributo. Para obter mais informações, consulte [Configurar tipos de atributo](attribute-properties-configure-attribute-types.md).|  
|`UnaryOperatorColumn`|Especifica a coluna que fornece operadores unários. É uma associação do tipo DataItem que define os detalhes de uma coluna fornecendo um operador unário.|  
|`Usage`|Descreve como um atributo é usado.<br /><br /> As opções disponíveis são as seguintes:<br /><br /> `Regular` O atributo é um atributo regular. Este é o valor padrão.<br /><br /> **Key** O atributo é um atributo de chave.<br /><br /> **Parent** O atributo é um atributo pai.|  
|`ValueColumn`|Identifica a coluna que fornece o valor do atributo. Se o `NameColumn` elemento do atributo for especificado, o mesmo `DataItem` valores são usados como valores padrão para o `ValueColumn` elemento. Se o elemento `NameColumn` do atributo não for especificado e a coleção `KeyColumns` do atributo contiver um elemento único `KeyColumn` representando uma coluna de chave com um tipo de dados de cadeia de caracteres, os mesmos valores `DataItem` serão usados como valores padrão para o elemento `ValueColumn`.|  
  
> [!NOTE]  
>  Para obter mais informações sobre como definir valores para o `KeyColumn` propriedade quando você estiver trabalhando com valores nulos e outros problemas de integridade de dados, consulte [Handling Data Integrity Issues in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
> [!NOTE]  
>  O membro padrão em um atributo será usado para avaliar as expressões quando um membro da hierarquia não for incluído explicitamente em uma consulta. O membro padrão para um atributo é especificado pelo `DefaultMember` propriedade no atributo. Sempre que uma hierarquia de uma dimensão for incluída em uma consulta, todos os membros padrão de atributos correspondentes a níveis na hierarquia serão ignorados. Se nenhuma hierarquia de uma dimensão for incluída em uma consulta, os membros padrão serão usados em todos os atributos da dimensão. Para obter mais informações, consulte [Definir um membro padrão](attribute-properties-define-a-default-member.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  