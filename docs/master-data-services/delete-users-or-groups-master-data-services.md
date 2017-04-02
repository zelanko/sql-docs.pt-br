---
title: "Excluir usu&#225;rios ou grupos (Master Data Services) | Microsoft Docs"
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
  - "excluindo grupos [Master Data Services]"
  - "grupos [Master Data Services], excluindo"
  - "usuários [Master Data Services], excluindo"
  - "excluindo usuários [Master Data Services]"
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Excluir usu&#225;rios ou grupos (Master Data Services)
  Exclua usuários ou grupos quando não desejar mais que eles acessem o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Observe o seguinte comportamento ao excluir usuários e grupos:  
  
-   Se você excluir um usuário que é membro de um grupo com acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ele ainda poderá acessar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] até que você o remova do Active Directory ou do grupo local.  
  
-   Se você excluir um grupo, todos os usuários do grupo que acessaram o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] serão exibidos na lista **Usuários** até que você os exclua.  
  
-   As alterações na segurança não são propagadas no MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] durante 20 minutos.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
### Para excluir usuários ou grupos  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Para excluir um usuário, permaneça na página **Usuários**. Para excluir um grupo, na barra de menus, clique em **Gerenciar Grupos**.  
  
3.  Na grade, selecione a linha correspondente ao usuário ou grupo que você deseja excluir.  
  
4.  Clique em **Excluir usuário selecionado** ou **Excluir grupo selecionado**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## Consulte também  
 [Segurança &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  