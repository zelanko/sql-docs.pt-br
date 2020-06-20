---
title: Reativar um membro ou coleção (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], reactivating
- consolidated members [Master Data Services], reactivating
- reactivating members [Master Data Services]
- members [Master Data Services], reactivating
- reactivating collections [Master Data Services]
- leaf members [Master Data Services], reactivating
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6fcbbca7703af5e254f295240888c2fa54938763
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960706"
---
# <a name="reactivate-a-member-or-collection-master-data-services"></a>Reativar um membro ou coleção (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode reativar um membro que estava:  
  
-   Desativado pelo processo de preparo.  
  
-   Excluído do MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
-   Excluído do aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
 Quando você reativa um membro, seus atributos e sua associação em hierarquias e coleções são restaurados.  
  
 Você também pode reativar coleções. Quando você fizer isso, são restaurados os atributos da coleção e os membros que pertencem à coleção.  
  
 Quando uma coleção ou membro é reativado, todas as transações anteriores são restauradas.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-reactivate-a-member-or-collection"></a>Para reativar um membro ou coleção  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , clique em **Gerenciamento de Versões**.  
  
2.  Na barra de menus, clique em **Transações**.  
  
3.  Na página **Transações** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Versão** , selecione uma versão.  
  
5.  No painel **Transações** , clique na linha do membro ou da coleção que você deseja reativar. Essa linha deve ter **Ativo** exibido na coluna **Valor Anterior** e **Desativado** na coluna **Novo Valor** .  
  
6.  Clique em **Inverter Transação**.  
  
7.  Na caixa de diálogo de confirmação, clique em **OK**. Uma nova transação é adicionada, mostrando **Ativo** na coluna **Novo Valor** .  
  
## <a name="see-also"></a>Consulte Também  
 [Desativar ou excluir membros usando o processo de preparo &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Excluir um membro ou uma coleção &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Coleções &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)  
  
  
