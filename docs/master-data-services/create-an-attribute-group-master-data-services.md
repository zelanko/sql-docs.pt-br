---
title: "Criar um grupo de atributo (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "grupos de atributos [Master Data Services], criação"
  - "criando grupos de atributos [Master Data Services]"
ms.assetid: 798c325e-e8d8-412a-b02e-118f2741d1c7
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Criar um grupo de atributo (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie grupos de atributos quando você desejar exibir atributos em guias individuais na grade do **Gerenciador** .  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Pelo menos um atributo deve existir. Para obter mais informações, consulte [Criar um atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md).  
  
### Para criar um grupo de atributo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , escolha um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , na grade, selecione a linha para a entidade para a qual você deseja criar o grupo de atributos.  
  
4.  Clique em **Grupos de Atributos**.  
  
5.  Na página Gerenciar Grupos de Atributos, execute um dos procedimentos a seguir e clique em **Adicionar**.  
  
     Se o grupo de atributo for destinado a membros folha, escolha **Folha** na lista suspensa **Tipos de Membro**, na parte superior da página.  
  
     Se o grupo de atributos for destinado a membros consolidados, selecione **Consolidado** na caixa suspensa **Tipos de Membro**.  
  
     Se o grupo de atributos for destinado a coleções, selecione **Coleção** na lista suspensa **Tipos de Membro**.  
  
6.  Clique em **Grupos de Folha**, **Grupos Consolidados**ou **Grupos de Coleção** para criar um grupo de atributos de membros folha, membros consolidados ou coleções, respectivamente.  
  
7.  Na caixa **Nome** , digite um nome para o grupo de atributos. Esse é o nome exibido na guia no **Explorer**.  
  
8.  Para adicionar um atributo, clique no atributo na caixa **Atributos Disponíveis** e clique na seta **Adicionar** . Para adicionar todos os atributos, clique na seta **Adicionar Tudo** .  
  
9. Clique nas setas **Para cima** e **Para baixo** para alterar a ordem dos atributos da esquerda para a direita.  
  
10. Clique nos usuários na caixa **Usuários Disponíveis** e clique na seta **Adicionar** . Para adicionar todos os usuários, clique na seta **Adicionar Tudo** .  
  
11. Clique nos grupos na caixa **Grupos Disponíveis** e clique na seta **Adicionar** . Para adicionar todos os grupos, clique na seta **Adicionar Tudo** .  
  
12. Clique em **Salvar**.  
  
## Próximas etapas  
  
-   [Tornar um grupo de atributos visível para os usuários &#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)  
  
## Consulte também  
 [Grupos de atributos &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Alterar o nome de um grupo de atributos &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)   
 [Excluir um grupo de atributos &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)   
 [Permissões de folha &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)   
 [Permissões consolidadas &#40;Master Data Services&#41;](../Topic/Consolidated%20Permissions%20\(Master%20Data%20Services\).md)  
  
  