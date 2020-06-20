---
title: Excluir permissões de objeto modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting model object permissions [Master Data Services]
- permissions [Master Data Services], deleting model object permissions
- models [Master Data Services], deleting object permissions
ms.assetid: 859c5952-f600-4940-8064-1afd13f7f6dc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: abb667d98ec3777a194226063ca4b203c8d83d02
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84950290"
---
# <a name="delete-model-object-permissions-master-data-services"></a>Excluir permissões de objeto modelo (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua as permissões do objeto de modelo para remover as atribuições feitas.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-model-object-permissions"></a>Para excluir permissões de objeto de modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Na página **Usuários** ou **Grupos** , selecione a linha do usuário ou grupo que deseja editar.  
  
3.  Clique em **Editar usuário selecionado**.  
  
4.  Clique na guia **Modelos** .  
  
5.  Opcionalmente, selecione um modelo na lista **Modelo** .  
  
6.  No painel **Resumo de permissões de modelo** , selecione a linha para a permissão que você deseja excluir.  
  
7.  Clique em **excluir permissão selecionada**.  
  
    > [!NOTE]  
    >  Você não poderá remover uma permissão de um usuário se a permissão for herdada de um grupo. Em vez disso, você deve remover a permissão do grupo.  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
  
