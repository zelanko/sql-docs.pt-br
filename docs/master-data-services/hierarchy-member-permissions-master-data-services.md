---
title: Permissões de membro de hierarquia
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], permissions
- permissions [Master Data Services], members
ms.assetid: b3880eed-1bf6-4f65-ab23-b08c194cc858
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 41fe545d2a70ea1cbe3ccd05bbbd06174552d3b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729240"
---
# <a name="hierarchy-member-permissions-master-data-services"></a>Permissões de membro de hierarquia (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  As permissões de membro de hierarquia são opcionais e devem ser usadas somente quando você desejar que um usuário tenha acesso limitado a membros específicos. Se você não atribuir permissões na guia **Membros da Hierarquia** , as permissões do usuário serão baseadas somente nas permissões atribuídas na guia **Modelos** .  
  
 As permissões de membro de hierarquia são [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] atribuídas na interface do usuário, na área funcional **permissões de usuário e grupo** na guia **membros da hierarquia** . Essas permissões determinam quais membros um usuário pode acessar na área funcional do **Gerenciador** da interface do usuário.  
  
 Na guia **Membros da Hierarquia** , cada hierarquia é representada como uma estrutura de árvore. Quando você atribuir permissão para um nó na árvore, todos os filhos herdam essa permissão a menos que ela seja atribuída explicitamente a um nível inferior.  
  
> [!NOTE]  
>  Quando você atribuir permissão para um nó em uma hierarquia, todos os membros de todos os outros nós no mesmo nível ou superior serão recusados implicitamente.  
  
 No **Gerenciador**, as permissões de membro são aplicadas em todos lugares em que o membro é exibido. Por exemplo, um membro com permissão de **leitura** pode ler quaisquer entidades, hierarquias e coleções às quais pertença.  
  
 As permissões de membro de hierarquia aplicam-se à versão do modelo que recebe as permissões, e a qualquer cópia futura da versão. Elas não se aplicam a versões anteriores a que você está atribuindo.  
  
|Permissão|DESCRIÇÃO|  
|----------------|-----------------|  
|**Ler**|Os membros são exibidos.<br /><br /> <br /><br /> Observação: se você atribuir apenas a permissão **Leitura** a **Raiz**, os membros sob **Raiz** serão somente leitura; porém, em hierarquias explícitas e coleções, o usuário poderá mover os membros para **Raiz** e adicionar novos membros a **Raiz**.|  
|**Criada**|A permissão Criar não está disponível na permissão de membro da hierarquia.|  
|**Cumulativo**|Os membros são exibidos e o usuário pode alterá-los. O usuário também pode mover os membros em qualquer hierarquia explícita ou coleções a que os membros pertencem.|  
|**Delete (excluir)**|Os membros são exibidos e o usuário pode excluí-los.|  
|**Deny**|Os membros não são exibidos.|  
  
 Na guia **Membros da Hierarquia** , as permissões que você atribui não entram em vigor imediatamente. A frequência com que as permissões são aplicadas depende da **Configuração de intervalo de processamento da segurança de membro** na tabela de Configurações do Sistema no banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . É possível aplicar permissões de membros imediatamente seguindo as etapas em [Aplicar permissões de membros imediatamente &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md).  
  
> [!NOTE]  
>  Não é possível atribuir permissões de membro de hierarquia a hierarquias recursivas, hierarquias derivadas com delimitações explícitas e a hierarquias derivadas com níveis ocultos.  
  
## <a name="possible-overlapping-permissions"></a>Permissões sobrepostas possíveis  
 Ao atribuir permissão para membros, pode ser necessário resolver permissões sobrepostas.  
  
### <a name="when-a-member-belongs-to-multiple-hierarchies"></a>Quando um membro pertence a várias hierarquias  
 Duas ou mais hierarquias podem conter o mesmo membro.  
  
-   Se um nó de hierarquia receber permissão **Atualizar** e outra receber **Leitura**, então os membros no nó serão **Leitura**.  
  
-   Se as permissões **Atualizar** e **Criar** forem atribuídas a um nó da hierarquia e outro receber as permissões **Atualizar** e **Excluir** , então os membros do nó poderão ser atualizados.  
  
-   Se um nó de hierarquia for atribuído a qualquer combinação de permissões **criar**/**leitura**/**Atualizar**/**excluir** e outro nó receber permissões **negar** , o acesso aos membros no nó será negado.  
  
## <a name="external-resources"></a>Recursos externos  
 Postagem do blog, [Aprimoramentos de Segurança](https://go.microsoft.com/fwlink/p/?LinkId=615376), em msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Hierarquias &#40;Master Data Services&#41;](../master-data-services/hierarchies-master-data-services.md)   
 [Aplicar permissões de membro imediatamente &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md)  
  
  
