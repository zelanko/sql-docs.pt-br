---
title: Classes de segurança AMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Analysis Management Objects, security
- security [AMO]
- AMO, security
ms.assetid: e3d5012a-8121-40de-9244-1fc824228693
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8ce9352890b4e1113278148a92c4802074f0d25
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047826"
---
# <a name="amo-security-classes"></a>Classes de segurança AMO
  
 A ilustração a seguir mostra o relacionamento das classes explicadas neste tópico.  
  
 ![Este tópico abrange as classes de segurança em AMO](../../../analysis-services/dev-guide/media/amo-securityclasses.gif "classes de segurança em AMO abordados neste tópico")  
  
##  <a name="RolesMembers"></a> Objetos role e RoleMember  
 Um objeto <xref:Microsoft.AnalysisServices.Role> é criado ao ser adicionado à coleção de funções do banco de dados e pela atualização do objeto <xref:Microsoft.AnalysisServices.Role> para o servidor por meio do método Update. Um objeto <xref:Microsoft.AnalysisServices.Role> deve ser atualizado antes de ser usado.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.Role>, ele terá de ser descartado por meio do método Drop do objeto <xref:Microsoft.AnalysisServices.Role>. O método Remove, da coleção de funções, só impede que você veja a função em seu aplicativo, mas não a remove do servidor. Um objeto <xref:Microsoft.AnalysisServices.Role> não poderá ser descartado se houver qualquer permissão associada a ele.  
  
 Um objeto <xref:Microsoft.AnalysisServices.RoleMember> é criado pela adição de um usuário à coleção de membros da função e pela atualização do objeto <xref:Microsoft.AnalysisServices.Role> para o servidor por meio do método Update. Somente os administradores de servidor ou os administradores de banco de dados podem criar funções. Um objeto <xref:Microsoft.AnalysisServices.Role> deve ser atualizado para o servidor antes que qualquer um de seus membros posa usar os objetos para os quais o usuário obteve permissão.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.RoleMember>, ele terá de ser removido da coleção por meio do método Remove da coleção e depois a função terá de ser atualizada por meio do método Update.  
  
 Para obter mais informações sobre os métodos e as propriedades disponíveis para esses objetos, consulte <xref:Microsoft.AnalysisServices.Role> e <xref:Microsoft.AnalysisServices.RoleMember> em <xref:Microsoft.AnalysisServices>.  
  
##  <a name="Permissions"></a> Objetos de permissão  
 Um objeto <xref:Microsoft.AnalysisServices.Permission> é criado ao ser adicionado à coleção de permissões do objeto e pela atualização do objeto <xref:Microsoft.AnalysisServices.Permission> para o servidor por meio do método Update.  
  
 Para remover um objeto <xref:Microsoft.AnalysisServices.Permission>, ele terá de ser descartado por meio do método Drop do objeto. O método de remoção, a partir da coleção de permissões, só impede que você veja a permissão em seu aplicativo, mas não remove o objeto <xref:Microsoft.AnalysisServices.Permission> do servidor. Uma função não poderá ser excluída se houver qualquer permissão associada a ela.  
  
 Para obter mais informações sobre os métodos e propriedades disponíveis, consulte <xref:Microsoft.AnalysisServices.Permission> em <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.AnalysisServices>   
 [Programando objetos de segurança AMO](programming-amo-security-objects.md)   
 [Permissões e direitos de acesso &#40;Analysis Services - dados multidimensionais&#41;](https://msdn.microsoft.com/library/ms174786(v=sql.120).aspx)   
 [Introdução às Classes AMO](amo-classes-introduction.md)   
 [Arquitetura lógica &#40; Analysis Services - dados multidimensionais &#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40; Analysis Services - dados multidimensionais &#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
