---
title: Configurar o nível (All) para hierarquias de atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 23b00a88c8abf80045a38d0b8cc5d0c695949b0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021673"
---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>Dimensões de banco de dados - Configure o nível (All) para hierarquias de atributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o nível (All) é um nível opcional gerado pelo sistema. Contém apenas um membro, cujo valor é a agregação de valores de todos os membros do nível imediatamente subordinado. Este membro é chamado de membro All. Trata-se de um membro gerado pelo sistema e que não é incluído na tabela de dimensões. Como o membro do nível (All) está no topo da hierarquia, seu valor é a agregação consolidada dos valores de todos os membros da hierarquia. Geralmente, o membro All funciona como membro padrão de uma hierarquia.  
  
 A existência de um nível (All) em uma hierarquia de atributos depende da configuração da propriedade **IsAggregatable** do atributo e a existência de um nível (All) na hierarquia definida pelo usuário depende da propriedade **IsAggregatable** do atributo em seu nível mais alto. Se a propriedade **IsAggregatable** estiver definida como **True**, haverá um nível (All). Uma hierarquia não terá nenhum nível (All) se a propriedade **IsAggregatable** estiver definida como **False**.  
  
## <a name="establishing-the-topmost-level"></a>Estabelecendo o nível mais alto  
 Se a propriedade **IsAggregatable** estiver definida como **False** no atributo de origem de um nível da hierarquia, nenhum nível agregável poderá aparecer acima dele na hierarquia. Um nível não agregável deve ser o nível mais alto de qualquer hierarquia ou a propriedade **IsAggregatable** dos atributos de origem de todos os níveis acima dele também deve ser definida como **False**.  
  
## <a name="all-member-and-all-level"></a>Membro e nível (All)  
 O único membro do nível (All) é chamado de membro All. A propriedade **AttributeAllMemberName**em uma dimensão especifica o nome do membro All para os atributos em uma dimensão. A propriedade **AllMemberName** em uma hierarquia especifica o nome do membro All da hierarquia.  
  
## <a name="see-also"></a>Consulte também  
 [Definir um membro padrão](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
