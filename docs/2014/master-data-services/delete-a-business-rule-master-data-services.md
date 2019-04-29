---
title: Excluir uma regra de negócios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 652b301a91adc3c6c417e23ff2f192712c5f4a04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62924959"
---
# <a name="delete-a-business-rule-master-data-services"></a>Excluir uma regra de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua uma regra de negócio quando ela não for mais necessária.  
  
> [!NOTE]  
>  Você pode evitar a validação de dados em relação a uma regra de negócio excluindo-a. Para obter mais informações, consulte [Exclude a Business Rule &#40;Master Data Services&#41;](exclude-a-business-rule-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-business-rule"></a>Para excluir uma regra de negócio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **Manutenção de Regra de Negócio** , na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Na lista **Tipo de Membro** , selecione um tipo de membro ao qual a regra de negócio será aplicada.  
  
6.  Na lista **Atributo** , selecione um atributo ou deixe o valor padrão **Todos**.  
  
7.  Na grade, clique na linha da regra de negócios que você deseja excluir.  
  
8.  Clique em **Excluir regra de negócio selecionada**.  
  
9. Na caixa de diálogo de confirmação, clique em **OK**. O valor de **Status** coluna é **exclusão pendente**.  
  
10. Clique em **Publicar regras de negócio**.  
  
11. Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir uma regra de negócio &#40;Master Data Services&#41;](exclude-a-business-rule-master-data-services.md)   
 [Criar e publicar uma regra de negócios &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  
