---
title: Definir um membro padrão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49120d810eac622d75a8d3691654b65b78d0d570
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537451"
---
# <a name="define-a-default-member"></a>Definir um membro padrão
  O membro padrão de uma hierarquia de atributo será usado para avaliar as expressões quando uma hierarquia de atributo não for explicitamente incluída em uma consulta. O membro padrão será ignorado sempre que a consulta tiver uma hierarquia de atributo ou hierarquia de usuário que contenha o atributo que dá origem à hierarquia de atributo. Isso porque será usado o membro especificado na consulta.  
  
 O membro padrão de uma hierarquia de atributo é definido pela especificação de um atributo membro como o valor da propriedade `DefaultMember` da hierarquia de atributo. Você pode definir essa propriedade na guia Estrutura da Dimensão do Designer de Dimensão ou no script de cálculo da guia Cálculo do Designer de Cubo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Também pode especificar a propriedade `DefaultMember` de uma função de segurança (substituindo o membro padrão definido na dimensão) na guia Dados da Dimensão ao definir a segurança da dimensão. Para evitar problemas de resolução de nome, defina o membro padrão no script MDX do cubo nas seguintes situações: se o cubo fizer referência a uma dimensão de banco de dados mais de uma vez; se os nomes da dimensão no cubo e no banco de dados forem diferentes; ou se você quiser ter membros padrão distintos em cubos diferentes.  
  
 O membro padrão em um atributo é usado para avaliar as expressões quando um atributo não for incluído em uma consulta. O membro padrão de um atributo é especificado pela sua propriedade `DefaultMember`. Sempre que uma hierarquia de uma dimensão for incluída em uma consulta, todos os membros padrão de atributos correspondentes a níveis na hierarquia serão ignorados. Se nenhuma hierarquia de uma dimensão for incluída em uma consulta, os membros padrão serão usados em todos os atributos da dimensão.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Resolvendo o membro padrão quando não houver um membro padrão especificado.  
 Se nenhum membro padrão for especificado para uma hierarquia de atributo e essa hierarquia de atributo for agregável (a propriedade `IsAggregatable` do atributo for definida como `True`), o membro (All) será o membro padrão. Se nenhum membro padrão for especificado e a hierarquia de atributo não for agregável (a propriedade `IsAggregatable` do atributo for definida como `False`), o membro padrão será selecionado no nível mais alto da hierarquia de atributo.  
  
## <a name="specifying-the-default-member"></a>Especificando o membro padrão  
 Cada atributo em uma dimensão no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem um membro padrão, que pode ser especificada usando o `DefaultMember` propriedade para um atributo. Essa configuração será usada para avaliar expressões se não houver um atributo incluído em uma consulta. Se a consulta especificar a hierarquia de uma dimensão, os membros padrão dos atributos da hierarquia serão ignorados. Se uma consulta não especificar uma hierarquia em uma dimensão, o `DefaultMember` configurações para atributos de dimensão entrem em vigor.  
  
 Se o `DefaultMember` configuração de um atributo estiver em branco e sua `IsAggregatable` estiver definida como `True`, o membro padrão será o membro All. Se o `IsAggregatable` estiver definida como `False`, o membro padrão será o primeiro membro do primeiro nível visível.  
  
 O `DefaultMember` configuração para um atributo se aplica a toda hierarquia na qual o atributo participa. Não é possível usar configurações diferentes para hierarquias diferentes em uma dimensão. Por exemplo, se o membro [1998] for o membro padrão do atributo [Ano], essa configuração será válida para todas as hierarquias da dimensão. O `DefaultMember` configuração nesse caso, não pode ser [1998] em uma hierarquia e [1997] em uma hierarquia diferente.  
  
 Se você definir um membro padrão para um determinado nível de uma hierarquia que não é agregada naturalmente, defina os membros padrão de todos os níveis acima desse nível da hierarquia. Por exemplo, na hierarquia todos-países-clima, você não pode definir um membro padrão para cada clima a menos que você defina um membro padrão para países. Se ele não for criado, ocorrerão erros de consulta-tempo.  
  
 Quando os níveis de uma hierarquia agregam-se naturalmente, você pode definir um membro padrão para qualquer atributo da hierarquia sem relação com os demais atributos da mesma. Por exemplo, na hierarquia de país-província-cidade, você pode definir um membro padrão para cidade, como [Cidade]. [São Paulo] sem definir o membro padrão para o estado ou país.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o nível &#40;All&#41; para hierarquias de atributo](database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
