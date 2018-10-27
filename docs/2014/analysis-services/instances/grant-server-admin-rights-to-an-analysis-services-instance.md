---
title: Conceder permissões de administrador de servidor (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8df7e950f300028b2246450bf29ed0e8776f2cd4
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145291"
---
# <a name="grant-server-administrator-permissions-analysis-services"></a>Conceder permissões de administrador do servidor (Analysis Services)
  Os membros da função de administrador de servidor em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] têm acesso ilimitado a todos os objetos e dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nessa instância. O usuário deve ser membro da função de administrador de servidor para realizar qualquer tarefa em todo o servidor, como criar ou processar um banco de dados, modificar propriedades do servidor ou iniciar um rastreamento (em vez de eventos de processamento).  
  
 A associação de função é estabelecida quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é instalado. O usuário que executa o programa de instalação pode adicioná-lo à função ou adicionar outro usuário, ao provisionar o servidor. Você pode modificar a associação de função como uma tarefa de pós-instalação usando o procedimento seguinte.  
  
## <a name="modify-server-role-membership"></a>Modificar a associação a funções de servidor  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], clique com o botão direito do mouse no nome da instância no Pesquisador de Objetos e clique em **Propriedades**.  
  
2.  Clique em **Segurança** no painel **Selecionar uma Página** . Depois, clique em **Adicionar** na parte inferior da página para adicionar um ou mais usuários ou grupos do Windows à função de servidor.  
  
     ![Caixa de diálogo Adicionar usuários no management studio](../media/ssas-serveradminadd.png "caixa de diálogo Adicionar usuários no management studio")  
  
 No momento da instalação, a Instalação do SQL Server exige que você especifique pelo menos uma conta de usuário como administrador de sistema do Analysis Services.  
  
 Por padrão, os membros do grupo Administradores local também recebem automaticamente direitos administrativos no Analysis Services. Embora o grupo local não seja explicitamente associado à função de administrador de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , os administradores locais podem criar bancos de dados, adicionar usuários e permissões, e executar qualquer outra tarefa permitida aos administradores do sistema. Esse comportamento é configurável. Ele é determinado pela `BuiltinAdminsAreServerAdmins` propriedade de servidor, que é definida como **verdadeiro** por padrão. Você pode alterar essa propriedade em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Security Properties](../server-properties/security-properties.md).  
  
 Também é possível gerenciar funções de servidor com o Analysis Management Objects (AMO). Para obter mais informações, consulte [Desenvolvendo com AMO &#40;Objetos de Gerenciamento de Análise&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).  
  
## <a name="see-also"></a>Consulte também  
 [Autorizando o acesso a objetos e operações &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Funções de Segurança &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
