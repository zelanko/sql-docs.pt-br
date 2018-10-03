---
title: Hierarquia pai-filho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], parent-child
- dimensions [Analysis Services], parent-child
- parent attributes [Analysis Services]
- data members [Analysis Services]
- hierarchies [Analysis Services], multilevel
- self-joins
- self-referencing relationships
- members [Analysis Services], data
- parent-child dimensions [Analysis Services]
ms.assetid: 4657f5dc-d88e-48d2-a448-08f79bc89546
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d20b40f89aeea9c4131ecc921754b1f1140d352c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124286"
---
# <a name="parent-child-hierarchy"></a>Hierarquia pai-filho
  Uma hierarquia pai-filho é uma hierarquia em uma dimensão padrão que contém um atributo pai. Um atributo pai descreve uma *relação de autorreferência*, ou *autojunção*, em uma tabela principal da dimensão. As hierarquias filho são construídas a partir de um único atributo pai. Somente um nível é atribuído a uma hierarquia pai-filho, pois os níveis existentes na hierarquia são extraídos das relações pai-filho entre os membros associados ao atributo pai. A posição de um membro em uma hierarquia pai-filho é determinada pelo `KeyColumns` e `RootMemberIf` propriedades do pai do atributo, enquanto a posição de um membro em um nível é determinada pela `OrderBy` propriedade do atributo pai. Para obter mais informações sobre as propriedades de atributo, consulte [Atributos e hierarquias de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
 Devido às relações pai-filho entre níveis de uma hierarquia pai-filho, alguns membros não folha também podem ter dados extraídos de fontes de dados subjacentes, além dos dados agregados dos membros filho.  
  
## <a name="dimension-schema"></a>Esquema de dimensão  
 O esquema de dimensão de uma hierarquia pai-filho depende de uma relação de autorreferência existente na tabela principal da dimensão. Por exemplo, o diagrama a seguir ilustra a tabela principal da dimensão **DimOrganization** do banco de dados de exemplo [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] .  
  
 ![Junção referenciada automaticamente na tabela DimOrganization](../dev-guide/media/dimorganization.gif "auto-referenciada de junção na tabela DimOrganization")  
  
 Nessa tabela de dimensão, a coluna **ParentOrganizationKey** possui uma relação de chave estrangeira com a coluna da chave primária **OrganizationKey** . Em outras palavras, cada registro dessa tabela pode ser relacionado por meio de uma relação pai-filho com outro registro da tabela. Geralmente, esse tipo de autojunção é usado para representar os dados de uma empresa, como a estrutura de gerenciamento dos funcionários de um departamento.  
  
## <a name="hierarchies-and-levels"></a>Hierarquias e níveis  
 Dimensões que não têm uma relação pai-filho criam hierarquias agrupando e ordenando atributos. Essas dimensões extraem os nomes dos níveis para suas hierarquias a partir dos nomes dos atributos.  
  
 Entretanto, dimensões pai-filho constroem hierarquias pai-filho analisando os dados contidos na tabela principal da dimensão e, em seguida, avaliando as relações pai-filho entre os registros da tabela. Para obter mais informações sobre hierarquias pai-filho, consulte [Hierarquias de usuários](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md).  
  
 As hierarquias pai-filho não extraem os nomes dos níveis de uma hierarquia pai-filho dos atributos usados para criar a hierarquia. Em vez disso, essas dimensões criam os nomes dos níveis automaticamente usando um modelo de nomeação — uma expressão de cadeia de caracteres que você especifica no nível do atributo pai e que controla como o atributo deve gerar sua hierarquia. Para obter mais informações sobre como definir o modelo de nomeação para um atributo pai, consulte [Atributos e hierarquias de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="data-members"></a>Membros de dados  
 Normalmente, os membros folha de uma dimensão contêm dados extraídos diretamente de fontes de dados subjacentes, enquanto os membros não folha contêm dados provenientes de agregações realizadas pelos membros filho.  
  
 No entanto, as hierarquias pai-filho devem ter alguns membros não folha cujos dados sejam provenientes de fontes de dados subjacentes, além dos dados agregados dos membros filho. Para esses membros não folha de uma hierarquia pai-filho, membros filho especiais gerados pelo sistema podem ser criados, contendo dados da tabela de fatos subjacente. Denominados *membros de dados*, esses membros filho especiais contêm um valor que é diretamente associado a um membro não folha e é independente do valor resumido calculado a partir dos descendentes do membro não folha. Para obter mais informações sobre membros de dados, consulte [Atributos em hierarquias pai-filho](parent-child-dimension-attributes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atributos em hierarquias pai-filho](parent-child-dimension-attributes.md)   
 [Propriedades de dimensão do banco de dados](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)  
  
  
