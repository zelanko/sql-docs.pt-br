---
title: "Classes de segurança AMO | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, security
- security [AMO]
- AMO, security
ms.assetid: e3d5012a-8121-40de-9244-1fc824228693
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c47924ca1262c6d6e283034ed281edf9e790b21b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="amo-security-classes"></a>Classes de segurança AMO
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Este tópico contém as seções a seguir:  
  
-   [Objetos role e RoleMember](#RolesMembers)  
  
-   [Objetos de permissão](#Permissions)  
  
 A ilustração a seguir mostra o relacionamento das classes explicadas neste tópico.  
  
 ![Classes de segurança em AMO abordados neste tópico](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-securityclasses.gif "classes de segurança em AMO abordados neste tópico")  
  
##  <a name="RolesMembers"></a>Objetos role e RoleMember  
 Um objeto <xref:Microsoft.AnalysisServices.Role> é criado ao ser adicionado à coleção de funções do banco de dados e pela atualização do objeto <xref:Microsoft.AnalysisServices.Role> para o servidor por meio do método Update. Um objeto <xref:Microsoft.AnalysisServices.Role> deve ser atualizado antes de ser usado.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.Role>, ele terá de ser descartado por meio do método Drop do objeto <xref:Microsoft.AnalysisServices.Role>. O método Remove, da coleção de funções, só impede que você veja a função em seu aplicativo, mas não a remove do servidor. Um objeto <xref:Microsoft.AnalysisServices.Role> não poderá ser descartado se houver qualquer permissão associada a ele.  
  
 Um objeto <xref:Microsoft.AnalysisServices.RoleMember> é criado pela adição de um usuário à coleção de membros da função e pela atualização do objeto <xref:Microsoft.AnalysisServices.Role> para o servidor por meio do método Update. Somente os administradores de servidor ou os administradores de banco de dados podem criar funções. Um objeto <xref:Microsoft.AnalysisServices.Role> deve ser atualizado para o servidor antes que qualquer um de seus membros posa usar os objetos para os quais o usuário obteve permissão.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.RoleMember>, ele terá de ser removido da coleção por meio do método Remove da coleção e depois a função terá de ser atualizada por meio do método Update.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis para esses objetos, consulte <xref:Microsoft.AnalysisServices.Role> e <xref:Microsoft.AnalysisServices.RoleMember> em <xref:Microsoft.AnalysisServices>.  
  
##  <a name="Permissions"></a>Objetos de permissão  
 Um objeto <xref:Microsoft.AnalysisServices.Permission> é criado ao ser adicionado à coleção de permissões do objeto e pela atualização do objeto <xref:Microsoft.AnalysisServices.Permission> para o servidor por meio do método Update.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.Permission>, ele terá de ser descartado por meio do método Drop do objeto. O método de remoção, a partir da coleção de permissões, só impede que você veja a permissão em seu aplicativo, mas não remove o objeto <xref:Microsoft.AnalysisServices.Permission> do servidor. Uma função não poderá ser excluída se houver qualquer permissão associada a ela.  
  
 Para obter mais informações sobre os métodos e propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Permission> em <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Programando objetos de segurança AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [Permissões e direitos de acesso &#40; Analysis Services - dados multidimensionais &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Introdução às Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
