---
title: Validar membros específicos em relação a regras de negócio (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ea749ca52eccf44b683b993be10607bdbc1c933
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Validar membros específicos em relação a regras de negócio (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], aplique regras de negócio seletivamente quando desejar atualizar ou validar subconjuntos de membros com base em regras de negócio.  
  
> [!NOTE]  
>  Se você deseja aplicar regras de negócio a todos os membros em uma versão de um modelo, consulte [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão **Atualizar** para o objeto de modelo ao qual está aplicando regras de negócio.  
  
### <a name="to-apply-business-rules-selectively"></a>Para aplicar regras de negócio seletivamente.  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista suspensa **Modelo** , selecione um modelo.  
  
2.  Na lista suspensa **Versão** , selecione uma versão.  
  
3.  Clique na guia **Gerenciador** .  
  
4.  Na barra de menus, aponte para **Entidades** e clique no nome da entidade que contém os membros aos quais você deseja aplicar regras.  
  
5.  Clique em **Aplicar Regras**. As regras de negócio são aplicadas apenas aos membros exibidos na grade.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
