---
title: "Segurança (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 56bc41ea-de28-4184-aa7e-99111ae55af5
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 4b540d7f5a204d6543bc32b5ec46fef766c9b973
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="security-master-data-services"></a>Segurança (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], use a segurança para garantir que os usuários tenham acesso aos dados mestre específicos necessários para fazer seus trabalhos e para impedir que acessem dados que não devem estar disponíveis para eles.  
  
 Você também pode usar segurança para transformar alguém em um administrador de um modelo e área funcional específicos (por exemplo, para permitir que alguém crie versões do modelo de Cliente ou para dar a alguém a capacidade de definir permissões de segurança).  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] é baseada em usuários e grupos do domínio local ou do Active Directory. A segurança do MDS permite que você use um nível granular de detalhes ao determinar os dados que um usuário pode acessar. Por causa da granularidade, a segurança pode se tornar facilmente complicada, e você deve ter cuidado ao usar sobreposição de usuários e grupos. Para obter mais informações, consulte [Sobrepondo permissões de usuário e grupo &#40;Master Data Services&#41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md).  
  
 Você pode atribuir acesso de segurança na área funcional **Permissões de Usuário e de Grupo** do aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou por meio do serviço Web.  
  
## <a name="types-of-users"></a>Tipos de usuários  
 Há dois tipos de usuários no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Os que acessam dados na área funcional **Gerenciador** .  
  
-   Os que têm a capacidade de executar tarefas administrativas em áreas diferentes do **Gerenciador**. Esses usuários são chamados [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
## <a name="how-to-set-security"></a>Como definir a segurança  
 Para dar permissão a um usuário ou grupo para acessar dados ou funcionalidade no MDS, você deve atribuir:  
  
-   [Acesso à área funcional](../master-data-services/functional-area-permissions-master-data-services.md), que determina quais das cinco áreas funcionais da interface do usuário podem ser acessadas pelo usuário.  
  
-   [Permissões de objeto de modelo](../master-data-services/model-object-permissions-master-data-services.md), que determinam os atributos que um usuário pode acessar e o tipo de acesso (Ler, Criar e Atualizar) que o usuário tem nesses atributos. O usuário também pode atribuir permissões de administrador no nível do modelo.  
  
-   Opcionalmente, [permissões de membro da hierarquia](../master-data-services/hierarchy-member-permissions-master-data-services.md), que determinam os membros que um usuário pode acessar e o tipo de acesso (Ler, Atualizar e Excluir) que o usuário tem nesses membros.  
  
 Quando você atribui permissões a atributos e membros, as permissões se cruzam e as regras determinam qual permissão tem precedência. Para obter mais informações, consulte [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md).  
  
## <a name="security-in-the-add-in-for-excel"></a>Segurança no suplemento para Excel  
 A segurança definida no aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] também se aplica ao [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Usuários só podem exibir e trabalhar com dados para os quais têm permissão. Administradores podem executar tarefas administrativas.  
  
 A única limitação é que toda a segurança atribuída no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] não entra em vigor no Excel antes de um intervalo de 20 minutos. O intervalo é definido pela configuração *MdsMaximumUserInformationCacheInterval* no arquivo web.config. Para alterar o intervalo, você pode alterar a configuração e reiniciar o IIS.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar um usuário que permissão total para um modelo.|[Criar um administrador de modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)|  
|Adicionar um grupo do Active Directory ao [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Essa é a primeira etapa ao dar uma permissão de grupo para acessar dados no aplicativo Web do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Adicionar um grupo &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)|  
|Atribuir permissão a uma área funcional do aplicativo Web do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Atribuir permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)|  
|Atribuir permissão a valores de atributos por meio da atribuição de permissão a objetos modelo.|[Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)|  
|Atribuir permissão a valores de membros por meio da atribuição de permissão a nós da hierarquia.|[Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [Usuários e grupos &#40;Master Data Services&#41;](../master-data-services/users-and-groups-master-data-services.md)   
 [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
