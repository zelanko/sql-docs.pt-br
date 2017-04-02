---
title: "Reativar um membro ou cole&#231;&#227;o (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "coleções [Master Data Services], reativando"
  - "membros consolidados [Master Data Services], reativando"
  - "reativando membros [Master Data Services]"
  - "membros [Master Data Services], reativando"
  - "reativando coleções [Master Data Services]"
  - "membros folha [Master Data Services], reativando"
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
caps.latest.revision: 11
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 11
---
# Reativar um membro ou cole&#231;&#227;o (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode reativar um membro que estava:  
  
-   Desativado pelo processo de preparo.  
  
-   Excluído do MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
-   Excluído do aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Quando você reativa um membro, seus atributos e sua associação em hierarquias e coleções são restaurados.  
  
 Você também pode reativar coleções. Quando você fizer isso, são restaurados os atributos da coleção e os membros que pertencem à coleção.  
  
 Quando uma coleção ou membro é reativado, todas as transações anteriores são restauradas.  
  
## Pré-requisitos  
 Para executar esse procedimento:  
  
-   No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você deve ter permissão para acessar a área funcional **Gerenciamento de Versões**.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### Para reativar um membro ou coleção  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , clique em **Gerenciamento de Versões**.  
  
2.  Na barra de menus, clique em **Transações**.  
  
3.  Na página **Transações** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Versão** , selecione uma versão.  
  
5.  No painel **Transações**, clique na linha do membro ou da coleção que você deseja reativar. Essa linha deve ter **Ativo** exibido na coluna **Valor Anterior** e **Desativado** na coluna **Novo Valor**.  
  
6.  Clique em **Inverter Transação**.  
  
7.  Na caixa de diálogo de confirmação, clique em **OK**. Uma nova transação é adicionada, mostrando **Ativo** na coluna **Novo Valor**.  
  
## Consulte também  
 [Excluir um membro ou uma coleção &#40;Master Data Services&#41;](../master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)   
 [Coleções &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
  