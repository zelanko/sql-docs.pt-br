---
title: Fatiar cubo de origem (Assistente de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6024c1e58b48c8661eaa15a0ea85c464103403ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326546"
---
# <a name="slice-source-cube-data-mining-wizard"></a>Fatiar cubo de origem (Assistente de Mineração de Dados)
  Você pode usar a caixa de diálogo **Fatiar Cubo de Origem** para restringir os dados usados para treinar o modelo. Normalmente, um cubo contém os dados relacionados a muitas dimensões e atributos diferentes, como todos os repositórios, todas as regiões e todos os produtos. Não é prático treinar um modelo em combinações ilimitadas de atributos; portanto, use essa caixa de diálogo para escolher um conjunto específico a ser usado no treinamento de um modelo.  
  
 Por exemplo, no cubo AdventureWorks, você pode fatiar por uma linha de produto, região ou ano específico, para obter uma parte dos dados.  
  
 Se você não estiver familiarizado com fatias e cubos, recomendamos consultar estes artigos:  
  
-   [Defina a propriedade fatia de partição &#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [Criar e gerenciar uma partição Local &#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  Observe que não há suporte para as funções MDX dinâmicas (como [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) ou [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function)) na propriedade Slice das partições. Você deve definir a fatia usando tuplas explícitas ou referências de membro.  
>   
>  Por exemplo, em vez de usar [: &#40;intervalo&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx) para definir um intervalo, você precisaria enumerar cada membro por anos específicos.  
>   
>  Se você precisa definir uma fatia complexa, recomendamos definir as tuplas na fatia usando um script XMLA Alter. Em seguida, você pode usar a ferramenta de linha de comando ascmd ou o SSIS [Analysis Services Execute DDL Task](../integration-services/control-flow/analysis-services-execute-ddl-task.md) para executar o script e criar o conjunto especificado de membros imediatamente antes de processar a partição.  
  
 **Para obter mais informações:** [Assistente de Mineração de Dados &#40;Analysis Services – Data Mining&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [Criar uma estrutura de mineração relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opções  
 **Dimension**  
 Selecione a dimensão que deseja fatiar.  
  
 **Hierarchy**  
 Selecione a hierarquia que deseja fatiar. Você pode escolher qualquer nível de uma hierarquia, mas os atributos usados no modelo estarão apenas no nível que você escolher.  
  
 Por exemplo, se você escolher a hierarquia Geography, e selecionar Country como o nível, não poderá criar um modelo que use City como os atributos. Por outro lado, se você escolher City como o nível da hierarquia onde poderá fatiar, não poderá criar um modelo de mineração baseado em Country.  
  
 **Operador**  
 Selecione o operador a ser usado para criar uma expressão da fatia.  
  
 Por exemplo, se você escolher Geography como a hierarquia, selecione o operador = e digite “Europe” como o filtro, para obter dados de cubo apenas para Europe.  
  
 **Expressão de filtro**  
 Digite uma expressão a ser usada como um critério para filtrar o cubo na dimensão selecionada.  
  
 **Parâmetros**  
 Esta opção não é usada para modelos de mineração de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Concluindo o Assistente de &#40;Assistente de mineração de dados&#41;](completing-the-wizard-data-mining-wizard.md)   
 [Ajuda F1 do Assistente de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Especificar o uso de colunas do modelo de mineração &#40;Assistente de mineração de dados&#41;](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
