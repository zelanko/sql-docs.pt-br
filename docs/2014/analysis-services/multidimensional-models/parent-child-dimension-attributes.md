---
title: Atributos em hierarquias pai-filho | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data members [Analysis Services]
- nonleaf members
- MembersWithDataCaption property
- members [Analysis Services]
- members [Analysis Services], data
- leaf members
- parent-child dimensions [Analysis Services]
- MembersWithData property
ms.assetid: 249971cc-4bcd-44f1-8241-bdacc04d3d38
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bbf5919d44a4e36e1bdddaf5c34c5e3ab6aa4315
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220276"
---
# <a name="attributes-in-parent-child-hierarchies"></a>Atributos em hierarquias pai-filho
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], normalmente é feita uma suposição geral sobre o conteúdo dos membros de uma dimensão. Membros folha contêm dados extraídos diretamente das fontes de dados subjacentes; membros não folha contêm dados provenientes de agregações realizadas pelos membros filho.  
  
 No entanto, em uma hierarquia pai-filho, alguns membros não folha também podem ter dados provenientes de fontes de dados subjacentes, além dos dados agregados dos membros filho. Para esses membros não folha de uma hierarquia pai-filho, são criados membros filho especiais gerados pelo sistema, contendo dados da tabela de fatos subjacente. Denominados *membros de dados*, eles contêm um valor que é diretamente associado a um membro não folha e é independente do valor resumido calculado a partir dos descendentes do membro não folha.  
  
 Os membros de dados ficam disponíveis somente para dimensões com hierarquias pai-filho e são visíveis apenas se o atributo pai permitir. Use o Designer de Dimensão para controlar a visibilidade de membros de dados. Para expor os membros de dados, defina a `MembersWithData` propriedade para o atributo pai como `NonLeafDataVisible.` para ocultar os membros de dados contidos pelo atributo pai, defina as `MembersWithData` propriedade no atributo pai como `NonLeafDataHidden`.  
  
 Essa configuração não substitui o comportamento de agregação normal de membros não folha; o membro de dados é sempre incluído como membro filho para a agregação. No entanto, uma fórmula de acúmulo personalizado pode ser usada para anular o comportamento de agregação normal. O MDX (Multidimensional Expressions) [DataMember](/sql/mdx/datamember-mdx) função fornece a capacidade de acessar o valor do membro de dados associado independentemente do valor da `MembersWithData` propriedade.  
  
 O `MembersWithDataCaption` propriedade do atributo pai fornece [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] com o modelo de nomeação usado para gerar nomes de membro para membros de dados.  
  
## <a name="using-data-members"></a>Usando membros de dados  
 Os membros de dados são úteis ao agregar medidas a dimensões organizacionais que possuem hierarquias pai-filho. Por exemplo, o diagrama a seguir mostra uma dimensão com três níveis, representando o volume de vendas brutas de produtos. O primeiro nível mostra o volume de vendas brutas de todos os vendedores. O segundo contém o volume de vendas brutas de todos os vendedores agrupados por gerente e o terceiro nível contém o volume de vendas brutas de todos os vendedores agrupado por vendedor.  
  
 ![Dimensão de volume de vendas brutas com três níveis](../media/agdatamember1.gif "dimensão de volume de vendas brutas com três níveis")  
  
 Em geral, o valor do membro Gerente de Vendas 1 seria proveniente da agregação dos valores dos membros Vendedores 1 e Vendedores 2. No entanto, como Gerente de Vendas 1 também pode vender produtos, ele também pode conter dados provenientes da tabela de fatos, pois haveria vendas brutas associadas a ele.  
  
 Além disso, as comissões de cada membro dos vendedores podem variar. Nesse caso, são usadas duas escalas diferentes para computar as comissões de cada venda bruta dos gerentes, diferente do total de vendas brutas gerado pelos vendedores. Portanto, é importante poder acessar os dados da tabela de fatos subjacente para membros não folha. O MDX `DataMember` função pode ser usada para recuperar o volume de vendas brutas individual do membro gerente de vendas 1 e uma expressão de acúmulo personalizado pode ser usada para excluir o membro de dados do valor agregado do membro gerente de vendas 1, fornecendo o valor bruto volume de vendas dos vendedores associados a esse membro.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de propriedades de atributo de dimensão](dimension-attribute-properties-reference.md)   
 [Hierarquia pai-filho](parent-child-dimension.md)  
  
  
