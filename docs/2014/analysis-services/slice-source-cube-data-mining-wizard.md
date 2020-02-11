---
title: Cubo de origem de fatia (Assistente de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.slicesourcecube.f1
ms.assetid: 16485608-d3b9-49ee-8baa-948038cdd7ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcb156d5c0a3c1332e748878ddebda1772b80696
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068603"
---
# <a name="slice-source-cube-data-mining-wizard"></a>Fatiar cubo de origem (Assistente de Mineração de Dados)
  Você pode usar a caixa de diálogo **Fatiar Cubo de Origem** para restringir os dados usados para treinar o modelo. Normalmente, um cubo contém os dados relacionados a muitas dimensões e atributos diferentes, como todos os repositórios, todas as regiões e todos os produtos. Não é prático treinar um modelo em combinações ilimitadas de atributos; portanto, use essa caixa de diálogo para escolher um conjunto específico a ser usado no treinamento de um modelo.  
  
 Por exemplo, no cubo AdventureWorks, você pode fatiar por uma linha de produto, região ou ano específico, para obter uma parte dos dados.  
  
 Se você não estiver familiarizado com fatias e cubos, recomendamos consultar estes artigos:  
  
-   [Definir a propriedade de fatia da partição &#40;Analysis Services&#41;](multidimensional-models/set-the-partition-slice-property-analysis-services.md)  
  
-   [Criar e gerenciar uma partição local &#40;Analysis Services&#41;](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
> [!NOTE]  
>  Observe que não há suporte para as funções MDX dinâmicas (como [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) ou [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function)) na propriedade Slice das partições. Você deve definir a fatia usando tuplas explícitas ou referências de membro.  
>   
>  Por exemplo, em vez de usar [: &#40;intervalo&#41; &#40;MDX&#41;](/sql/mdx/range-mdx) para definir um intervalo, você precisaria enumerar cada membro pelos anos específicos.  
>   
>  Se você precisa definir uma fatia complexa, recomendamos definir as tuplas na fatia usando um script XMLA Alter. Em seguida, você pode usar a ferramenta de linha de comando ascmd ou [Analysis Services Execute DDL Task](../integration-services/control-flow/analysis-services-execute-ddl-task.md) do SSIS para executar o script e criar o conjunto especificado de membros imediatamente antes de você processar a partição.  
  
 **Para obter mais informações:** [Assistente de mineração de dados &#40;Analysis Services&#41;de mineração de dados ](data-mining/data-mining-wizard-analysis-services-data-mining.md), [criar uma estrutura de mineração relacional](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opções  
 **Dimensão**  
 Selecione a dimensão que deseja fatiar.  
  
 **Hierarquia**  
 Selecione a hierarquia que deseja fatiar. Você pode escolher qualquer nível de uma hierarquia, mas os atributos usados no modelo estarão apenas no nível que você escolher.  
  
 Por exemplo, se você escolher a hierarquia Geography, e selecionar Country como o nível, não poderá criar um modelo que use City como os atributos. Por outro lado, se você escolher City como o nível da hierarquia onde poderá fatiar, não poderá criar um modelo de mineração baseado em Country.  
  
 **Operador**  
 Selecione o operador a ser usado para criar uma expressão da fatia.  
  
 Por exemplo, se você escolher geografia como a hierarquia, poderá selecionar o operador = e, em seguida, digitar "Europa" como filtro, para obter dados de cubo apenas para a Europa.  
  
 **Expressão de filtro**  
 Digite uma expressão a ser usada como um critério para filtrar o cubo na dimensão selecionada.  
  
 **Parâmetros**  
 Esta opção não é usada para modelos de mineração de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Concluindo o assistente &#40;assistente de mineração de dados&#41;](completing-the-wizard-data-mining-wizard.md)   
 [Ajuda F1 do assistente de mineração de dados &#40;Analysis Services Data Mining&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Especificar o uso de coluna do modelo de mineração &#40;assistente de mineração de dados&#41;](specify-mining-model-column-usage-data-mining-wizard.md)  
  
  
