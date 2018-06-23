---
title: Propriedades de estrutura de mineração e colunas de estrutura | Microsoft Docs
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
- mining structures [Analysis Services], column properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- properties [data mining]
ms.assetid: ce90f684-bb8c-4eca-b9e6-000794dbee16
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 167e04eb8623e6d2f7f11c3bfd43e3d6427c5886
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118002"
---
# <a name="properties-for-mining-structure-and-structure-columns"></a>Propriedades para estruturas de mineração e colunas de estrutura
  Você pode definir ou alterar as propriedades de uma estrutura de mineração e das colunas associadas e tabelas aninhadas usando a guia **Estrutura de Mineração** do Designer de Data Mining. As propriedades que você estabelece nesta guia se propagam para todo o modelo de mineração associado à estrutura.  
  
> [!NOTE]  
>  Se você alterar o valor de qualquer propriedade na estrutura de mineração, até mesmo metadados, como, por exemplo, um nome ou uma descrição, a estrutura de mineração e seus modelos deverão ser reprocessados para que você possa exibir ou consultar o modelo.  
  
## <a name="properties-of-mining-structures-and-mining-structure-columns"></a>Propriedades de estruturas de mineração e colunas de estrutura de mineração  
 A tabela a seguir descreve as propriedades específicas à estrutura de mineração e às colunas de estrutura de mineração que são específicas à mineração de dados e que você pode exibir ou configurar na guia **Estrutura de Mineração** . Para exibir ou configurar essas propriedades, clique com o botão direito do mouse em um elemento no modo de exibição de árvore e clique em **Propriedades**.  
  
-   Para exibir as propriedades da estrutura, clique no cabeçalho da estrutura de mineração.  
  
-   Para exibir as propriedades de uma coluna ou de uma tabela aninhada, clique no nome de coluna.  
  
### <a name="properties-of-the-mining-structure"></a>Propriedades da Estrutura de Mineração  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**CacheMode**|Especifica se os casos usados no treinamento devem ser colocados em cachê ou descartados após a conclusão do treinamento.<br /><br /> Observação: Essa propriedade deve ser definida como `KeepTrainingCases` para habilitar o detalhamento e validação.|  
|**Agrupamento**|Especifica o agrupamento padrão para a coluna. Se um agrupamento não for especificado, o agrupamento do servidor será usado.|  
|**Descrição**|Descreve a estrutura de mineração. Como uma prática recomendada, a descrição deve declarar o propósito e a composição dos dados na estrutura.|  
|**ErrorConfiguration (padrão)**|Especifica opções para manipulação especial de erros, se houver.|  
|**HoldoutMaxCases**|Especifica o número de máximo de casos de estrutura que podem ser reservados como uns conjunto de dados de testes.  Se forem especificados valores para **HoldoutMaxCases** e **HoldoutPercent**, as condições serão combinadas.<br /><br /> Observação: Para definir essa propriedade, <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> deve ser definido como `KeepTrainingCases`.|  
|**HoldoutPercent**|Especifica a porcentagem dos casos de estrutura a ser reservada como um conjunto de dados de testes. Se forem especificados valores para **HoldoutMaxCases** e **HoldoutPercent**, as condições serão combinadas.<br /><br /> Observação: Para definir essa propriedade, <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> deve ser definido como `KeepTrainingCases`.|  
|**HoldoutSeed**|Especifica uma semente para inicializar o particionamento do conjunto de teste de validação, a fim de garantir que o conjunto de dados de testes possa ser criado novamente.<br /><br /> Observação: Para definir essa propriedade, <xref:Microsoft.AnalysisServices.MiningStructure.CacheMode%2A> deve ser definido como `KeepTrainingCases`.|  
|**ID**|Exibe o identificador exclusivo da estrutura de mineração.<br /><br /> O nome que você atribuiu à estrutura de mineração quando você criou que a estrutura é usado como ID. Se, mais tarde, você alterar o nome digitando um novo valor para a propriedade `Name`, o novo nome será usado apenas como um alias; a ID não é alterada.|  
|**Idioma**|Especifica o idioma das legendas na estrutura de mineração.|  
|`Name`|Especifica o nome ou o alias da estrutura de mineração.<br /><br /> Se você alterar o valor da propriedade Name, o novo nome será usado apenas como uma legenda ou um alias; a identificação da estrutura de mineração não é alterada.|  
|**Origem**|Exibe o nome da origem de dados e o tipo de origem de dados.|  
  
### <a name="properties-of-the-mining-structure-columns"></a>Propriedades das colunas da estrutura de mineração  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**ClassifiedColumns**|Identifica a coluna descrita por uma coluna classificada.|  
|**Conteúdo**|O tipo de conteúdo da coluna.|  
|**Descrição**|Descreve a coluna. Como uma prática recomendada, a descrição da coluna deve fornecer informações sobre como os dados da coluna foram derivados ou alterados para mineração de dados.|  
|**DiscretizationBucketCount**|Exibe o número de recipientes na coluna de dados discretos.<br /><br /> Habilitada somente se o tipo de conteúdo é definido como `Discretized`.<br /><br /> Esta propriedade é somente leitura.|  
|**DiscretizationMethod**|Exibe o método usado para diferenciar a coluna.<br /><br /> Habilitada somente se o tipo de conteúdo é definido como `Discretized`.<br /><br /> Esta propriedade é somente leitura.|  
|**Distribuição**|Especifica a distribuição de conteúdo na coluna.|  
|**ID**|Exibe o identificador da coluna.<br /><br /> Se você alterar o valor da propriedade Name da coluna, o valor da propriedade ID não será afetado.|  
|**IsKey**|Indica se a coluna é uma coluna de chave.|  
|**KeyColumns**|Contém a definição de uma coluna que é a chave para um atributo, ou faz parte da chave.|  
|**ModelingFlags**|Define parâmetros adicionais disponibilizados pelo algoritmo.|  
|`Name`|O nome da coluna.|  
|**NameColumn**|Identifica a coluna que fornece o nome do elemento pai.|  
|**Origem**|Exibe a origem da coluna.<br /><br /> Para fontes de dados relacionais, o valor é sempre **(nenhum)**.<br /><br /> Para estruturas baseadas em um cubo OLAP, o valor é a instrução MDX que define a fatia usada como a origem da tabela aninhada.|  
|**SourceMeasureGroup**|Exibe a origem do grupo de medidas.<br /><br /> Para fontes de dados relacionais, o valor é sempre **(nenhum)**.<br /><br /> Para estruturas baseadas em um cubo OLAP, o valor é a instrução MDX que define a fatia usada como a origem da tabela aninhada.|  
|**Tipo**|O tipo de dados para o conteúdo na coluna.|  
  
 Para obter mais informações sobre a definição ou alteração de propriedades, consulte [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma estrutura de mineração relacional](create-a-relational-mining-structure.md)   
 [Colunas da estrutura de mineração](mining-structure-columns.md)  
  
  