---
title: Criar um administrador de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4032a624d49cbf7c70d710b6b4df7373353f1d2a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099156"
---
# <a name="create-a-model-administrator-master-data-services"></a>Criar um administrador de modelo (Master Data Services)
  Na [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um administrador de modelo quando desejar que um grupo ou usuário ter **atualização** permissão a todos os objetos em um ou mais modelos.  
  
> [!TIP]  
>  Para simplificar a administração, crie um grupo local ou do Windows e configure-o como um administrador de modelo. Isso lhe permitirá adicionar e remover usuários do grupo sem acessar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-create-a-model-administrator"></a>Para criar um administrador de modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Na página **Usuários** ou **Grupos** , selecione a linha do usuário ou grupo que deseja editar.  
  
3.  Clique em **Editar usuário selecionado**.  
  
4.  Clique na guia **Modelos** .  
  
5.  Opcionalmente, selecione um modelo na lista **Modelo** .  
  
6.  Clique em **Editar**.  
  
7.  Clique no modelo ao qual você deseja atribuir permissão.  
  
8.  No menu, selecione **atualização**.  
  
9. Conclua as etapas 7 e 8 para cada modelo do qual o grupo ou usuário deverá ser administrador.  
  
10. Clique em **Salvar**.  
  
## <a name="remarks"></a>Comentários  
 Não atribua qualquer outra permissão a objetos de modelo ou membros de hierarquia. Se você fizer isso, o usuário não é mais um administrador e não é possível exibir o modelo em qualquer área funcional diferente de **Explorer**.  
  
 Há uma exceção: se o usuário tiver **atualização** permissão atribuída a uma hierarquia **raiz** no **membros da hierarquia** guia, o usuário ainda é considerado um modelo como administrador.  
  
## <a name="see-also"></a>Consulte também  
 [Os administradores de &#40;Master Data Services&#41;](administrators-master-data-services.md)   
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
