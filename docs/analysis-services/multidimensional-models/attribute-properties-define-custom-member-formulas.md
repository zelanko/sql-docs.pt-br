---
title: Definir fórmulas de membro personalizado | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 74db16133a17fbcb5d0cc013206a053f652c9000
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="attribute-properties---define-custom-member-formulas"></a>Propriedades de atributo - definir fórmulas de membro personalizado
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  É possível definir uma expressão multidimensional (MDX), chamada fórmula de membro personalizado, para fornecer os valores aos membros de um atributo especificado. Uma coluna em uma tabela da exibição da fonte de dados fornece, para cada membro de um atributo, a expressão usada para fornecer o valor para esse membro.  
  
 As fórmulas de membro personalizado determinam os valores de células associados aos membros e substituem as funções de agregação de medidas. Fórmulas de membro personalizado são escritas no formato MDX. Cada fórmula de membro personalizado é válida para um único membro. As fórmulas de membro personalizado são armazenadas na tabela de dimensões ou em outra tabela que tenha uma relação de chave estrangeira com a tabela de dimensões.  
  
 A propriedade **CustomRollupColumn** de um atributo especifica a coluna que contém fórmulas de membro personalizado para os membros do atributo. Se uma linha da coluna estiver vazia, o valor de célula do membro será retornado normalmente. Se a fórmula da coluna não for válida, ocorrerá um erro de tempo de execução sempre que o valor de uma célula que usa o membro for recuperado.  
  
 Antes de poder especificar fórmulas de membro personalizado para um atributo, confirme se a tabela de dimensões contém o atributo, ou uma tabela diretamente relacionada, possui uma coluna de cadeia de caracteres para armazenar as fórmulas de membro personalizado. Se for o caso, você pode configurar a propriedade **CustomRollupColumn** de um atributo manualmente ou usar o aprimoramento de Definir Fórmula de Membro Personalizado do Assistente de Business Intelligence para usar uma fórmula de membro personalizado em um atributo. Para obter mais informações sobre como usar essa melhoria, consulte [Definir fórmulas de membro personalizado para os atributos de uma dimensão](../../analysis-services/multidimensional-models/bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md).  
  
## <a name="evaluating-custom-member-formulas"></a>Avaliando fórmulas de membro personalizado  
 Fórmulas de membro personalizado são diferentes de membros calculados. As fórmulas de membro personalizado aplicam-se a membros que existem em tabelas de dimensões e fornecem apenas o valor do membro. Diferentemente, os membros calculados não são armazenados em tabelas de dimensões e as expressões de membros calculados definem os dados e os metadados para membros adicionais incluídos em uma dimensão ou hierarquia.  
  
 Fórmulas de membro personalizado substituem as funções de agregação associadas às medidas. Por exemplo, antes que uma fórmula de membro personalizado seja especificada, uma medida que usa a função de agregação **Sum** possuirá os valores a seguir para os seguintes membros da dimensão Tempo:  
  
-   2003: 2100  
  
    -   Trimestre 1: 700  
  
    -   Trimestre 2: 500  
  
    -   Trimestre 3: 100  
  
    -   Trimestre 4: 800  
  
-   2004: 1500  
  
    -   Trimestre 1: 600  
  
    -   Trimestre 2: 200  
  
    -   Trimestre 3: 300  
  
    -   Trimestre 4: 400  
  
 Com uma fórmula de membro personalizado, o valor do membro é fornecido pela fórmula de acúmulo personalizado. Por exemplo, a fórmula de membro personalizado a seguir pode ser usada para fornecer o valor de 450 para o membro filho Trimestre 4 do membro 2004 da dimensão Tempo.  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 As fórmulas de membro personalizado são armazenadas em uma coluna da tabela de dimensões. Habilite fórmulas de acúmulo personalizado configurando a propriedade **CustomRollupColumn** de um atributo.  
  
 Para aplicar a mesma expressão MDX a todos os membros de um atributo, crie um cálculo nomeado na tabela de dimensões que retorne uma expressão MDX como cadeia de caracteres literal. Em seguida, especifique o cálculo nomeado configurando a propriedade **CustomRollupColumn** no atributo que você quer configurar. Um cálculo nomeado é uma coluna da tabela de exibição da fonte de dados que retorna os valores de linha definidos por uma expressão SQL. Para obter mais informações sobre como construir cálculos nomeados, consulte [Definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
> [!NOTE]  
>  Para aplicar uma expressão MDX aos membros de um determinado nível e não aos membros de todos os níveis com base em um atributo em particular, defina a expressão como um script MDX no nível. Para obter mais informações, consulte [Conceitos básicos do script MDX &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).  
  
 Se você usar membros calculados e fórmulas de acúmulo personalizado para os membros de um atributo, não deixe de ordenar a avaliação. Membros calculados são resolvidos antes das fórmulas de acúmulo personalizado.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Definir fórmulas de membro personalizado para os atributos em uma dimensão](../../analysis-services/multidimensional-models/bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  
