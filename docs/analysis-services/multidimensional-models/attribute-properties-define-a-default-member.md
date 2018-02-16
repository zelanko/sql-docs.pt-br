---
title: "Definir um membro padrão | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a457e54c1653cfc996de2040a09e8b22578307f0
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="attribute-properties---define-a-default-member"></a>Propriedades de atributo - definir um membro padrão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
O membro padrão de uma hierarquia de atributo será usado para avaliar as expressões quando uma hierarquia de atributo não for explicitamente incluída em uma consulta. O membro padrão será ignorado sempre que a consulta tiver uma hierarquia de atributo ou hierarquia de usuário que contenha o atributo que dá origem à hierarquia de atributo. Isso porque será usado o membro especificado na consulta.  
  
 O membro padrão de uma hierarquia de atributo é definido pela especificação de um atributo membro como o valor da propriedade **DefaultMember** da hierarquia de atributo. Você pode definir essa propriedade na guia Estrutura da Dimensão do Designer de Dimensão ou no script de cálculo da guia Cálculo do Designer de Cubo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Também pode especificar a propriedade **DefaultMember** de uma função de segurança (substituindo o membro padrão definido na dimensão) na guia Dados da Dimensão ao definir a segurança da dimensão. Para evitar problemas de resolução de nome, defina o membro padrão no script MDX do cubo nas seguintes situações: se o cubo fizer referência a uma dimensão de banco de dados mais de uma vez; se os nomes da dimensão no cubo e no banco de dados forem diferentes; ou se você quiser ter membros padrão distintos em cubos diferentes.  
  
 O membro padrão em um atributo é usado para avaliar as expressões quando um atributo não for incluído em uma consulta. O membro padrão de um atributo é especificado pela sua propriedade **DefaultMember** . Sempre que uma hierarquia de uma dimensão for incluída em uma consulta, todos os membros padrão de atributos correspondentes a níveis na hierarquia serão ignorados. Se nenhuma hierarquia de uma dimensão for incluída em uma consulta, os membros padrão serão usados em todos os atributos da dimensão.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Resolvendo o membro padrão quando não houver um membro padrão especificado.  
 Se nenhum membro padrão for especificado para uma hierarquia de atributo e essa hierarquia de atributo for agregável (a propriedade **IsAggregatable** do atributo for definida como **True**), o membro (All) será o membro padrão. Se nenhum membro padrão for especificado e a hierarquia de atributo não for agregável (a propriedade **IsAggregatable** do atributo for definida como **False**), o membro padrão será selecionado no nível mais alto da hierarquia de atributo.  
  
## <a name="specifying-the-default-member"></a>Especificando o membro padrão  
 Todo atributo de uma dimensão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem um membro padrão, que você pode especificar usando a propriedade **DefaultMember** de um atributo. Essa configuração será usada para avaliar expressões se não houver um atributo incluído em uma consulta. Se a consulta especificar a hierarquia de uma dimensão, os membros padrão dos atributos da hierarquia serão ignorados. Se a consulta não especificar uma hierarquia de uma dimensão, as configurações de **DefaultMember** dos atributos da dimensão serão válidas.  
  
 Se a configuração **DefaultMember** de um atributo estiver em branco e a propriedade **IsAggregatable** for configurada como **True**, o membro padrão será o membro All. Se a propriedade **IsAggregatable** for configurada como **False**, o membro padrão será o primeiro membro do primeiro nível visível.  
  
 A configuração **DefaultMember** de um atributo é válida para toda hierarquia da qual o atributo participa. Não é possível usar configurações diferentes para hierarquias diferentes em uma dimensão. Por exemplo, se o membro [1998] for o membro padrão do atributo [Ano], essa configuração será válida para todas as hierarquias da dimensão. Neste caso, a configuração **DefaultMember** não pode ser [1998] em uma hierarquia e [1997] em outra.  
  
 Se você definir um membro padrão para um determinado nível de uma hierarquia que não é agregada naturalmente, defina os membros padrão de todos os níveis acima desse nível da hierarquia. Por exemplo, na hierarquia Todos-Países-Clima, não é possível definir um membro padrão para cada Clima a menos que você defina um membro padrão para Países. Se ele não for criado, ocorrerão erros de consulta-tempo.  
  
 Quando os níveis de uma hierarquia agregam-se naturalmente, você pode definir um membro padrão para qualquer atributo da hierarquia sem relação com os demais atributos da mesma. Por exemplo, na hierarquia País-Estado-Cidade, é possível definir um membro padrão para Cidade, como [Cidade] [São Paulo] sem definir o membro padrão para Estado ou País.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o &#40; Todos os &#41; Nível para hierarquias de atributo](../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
