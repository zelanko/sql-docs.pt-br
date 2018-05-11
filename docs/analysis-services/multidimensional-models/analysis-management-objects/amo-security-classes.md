---
title: Classes de segurança AMO | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3528ee142714b5efde841c4f4ef712be0ccb5748
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="amo-security-classes"></a>Classes de segurança AMO
  Este tópico contém as seguintes seções:  
  
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
 [Permissões e direitos de acesso & #40; Analysis Services - dados multidimensionais & #41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Introdução às Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Arquitetura lógica & #40; Analysis Services - dados multidimensionais & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
