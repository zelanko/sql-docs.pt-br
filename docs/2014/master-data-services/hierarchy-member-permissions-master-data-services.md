---
title: Permissões de membro de hierarquia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a8a50ce407e0f9284d07a7248f08decacf434fee
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971406"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>Permissões de membro de hierarquia (Master Data Services)
  As permissões de membro de hierarquia são opcionais e devem ser usadas somente quando você desejar que um usuário tenha acesso limitado a membros específicos. Se você não atribuir permissões na guia **Membros da Hierarquia** , as permissões do usuário serão baseadas somente nas permissões atribuídas na guia **Modelos** .  
  
 As permissões de membro de hierarquia são atribuídas na [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] interface do usuário, na área funcional **permissões de usuário e grupo** na guia **membros da hierarquia** . Essas permissões determinam quais membros um usuário pode acessar na área funcional do **Gerenciador** da interface do usuário.  
  
 Na guia **Membros da Hierarquia** , cada hierarquia é representada como uma estrutura de árvore. Quando você atribuir permissão para um nó na árvore, todos os filhos herdam essa permissão a menos que ela seja atribuída explicitamente a um nível inferior.  
  
> [!NOTE]  
>  Quando você atribuir permissão para um nó em uma hierarquia, todos os membros de todos os outros nós no mesmo nível ou superior serão recusados implicitamente.  
  
 No **Gerenciador**, as permissões de membro são aplicadas em todos lugares em que o membro é exibido. Por exemplo, um membro com permissão **somente leitura** é somente leitura em quaisquer entidades, hierarquias e coleções às quais ele pertence.  
  
 As permissões de membro de hierarquia aplicam-se à versão do modelo que recebe as permissões, e a qualquer cópia futura da versão. Elas não se aplicam a versões anteriores a que você está atribuindo.  
  
|Permissão|Descrição|  
|----------------|-----------------|  
|**Somente leitura**|Os membros são exibidos, mas o usuário não pode alterá-los. O usuário também não pode mover os membros em qualquer hierarquia explícita ou coleções a que os membros pertencem.<br /><br /> Observação: se você atribuir permissão **somente leitura** à **raiz**, os membros em **raiz** serão somente leitura; no entanto, em hierarquias explícitas e coleções, o usuário pode mover membros para **raiz** e pode adicionar novos membros à **raiz**.|  
|**Atualização**|Os membros são exibidos e o usuário pode alterá-los. O usuário também pode mover os membros em qualquer hierarquia explícita ou coleções a que os membros pertencem.|  
|**Deny**|Os membros não são exibidos.|  
  
 Na guia **Membros da Hierarquia** , as permissões que você atribui não entram em vigor imediatamente. A frequência com que as permissões são aplicadas depende da **Configuração de intervalo de processamento da segurança de membro** na tabela de Configurações do Sistema no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . É possível aplicar permissões de membros imediatamente seguindo as etapas em [Aplicar permissões de membros imediatamente &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md).  
  
> [!NOTE]  
>  Não é possível atribuir permissões de membro de hierarquia a hierarquias recursivas, hierarquias derivadas com delimitações explícitas e a hierarquias derivadas com níveis ocultos.  
  
## <a name="possible-overlapping-permissions"></a>Permissões sobrepostas possíveis  
 Ao atribuir permissão para membros, pode ser necessário resolver permissões sobrepostas.  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>Quando um membro pertence a várias hierarquias  
 Duas ou mais hierarquias podem conter o mesmo membro.  
  
-   Se uma permissão **Update** for atribuída a um nó de hierarquia e outra for atribuída **somente leitura**, os membros do nó serão **somente leitura**.  
  
-   Se uma permissão **Update** ou **somente leitura** for atribuída a um nó de hierarquia e outro nó for atribuído **negado**, os membros do nó não serão exibidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Hierarquias &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchies-master-data-services.md)   
 [Aplicar permissões de membros imediatamente &#40;Master Data Services&#41;](immediately-apply-member-permissions-master-data-services.md)  
  
  
