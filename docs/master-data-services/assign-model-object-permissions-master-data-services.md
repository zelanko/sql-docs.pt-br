---
title: "Atribuir permiss&#245;es de objeto modelo (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modelos [Master Data Services], atribuindo permissões de objeto"
  - "permissões [Master Data Services], atribuindo permissões de objeto de modelo"
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Atribuir permiss&#245;es de objeto modelo (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], atribua permissões a objetos modelo quando você precisar fornecer a um usuário ou grupo o acesso aos dados na área funcional **Explorer** do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ou quando precisar tornar um usuário ou grupo um administrador.  
  
> [!NOTE]  
>  Quando você atribui permissão a um modelo, a permissão a todos os outros modelos é negada implicitamente. Se você não atribuir permissões a objetos de modelo, o usuário ou grupo não poderá acessar nenhum dado no **Explorer**.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### Para atribuir permissões de objeto de modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Na página **Usuários** ou **Grupos** , selecione a linha do usuário ou grupo que deseja editar.  
  
3.  Clique em **Editar usuário selecionado**.  
  
4.  Clique na guia **Modelos** .  
  
5.  Opcionalmente, selecione um modelo na lista **Modelo** .  
  
6.  Clique em **Editar**.  
  
7.  Expanda a árvore e clique no objeto de modelo ao qual deseja atribuir permissões.  
  
8.  No menu, selecione uma combinação de Ler, Criar, Atualizar e Excluir ou Negar.  
  
9. No nível de modelo superior, selecione **Administrador** se precisar transformar um usuário em administrador de modelo.  
  
10. Clique em **Salvar**.  
  
## Próximas etapas  
  
-   (Opcional) [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## Consulte também  
 [Excluir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/delete-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Criar um administrador de modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)  
  
  