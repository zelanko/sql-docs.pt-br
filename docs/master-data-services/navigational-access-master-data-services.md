---
title: "Acesso de navegação (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- navigational access [Master Data Services]
- security [Master Data Services], navigational access
ms.assetid: 3403b7b0-44e2-48c3-a1b7-9c4612b874b8
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 7a26c6e03d53fcd619446a82b2d2196476d159dc
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="navigational-access-master-data-services"></a>Acesso de navegação (Master Data Services)
  O acesso de navegação se aplica à segurança do objeto do modelo que é atribuída na guia **Modelos** .  
  
 O acesso de navegação é o acesso que você obtém a níveis mais altos do que o acesso ao qual você atribuiu segurança.  
  
 Neste exemplo, as permissões são atribuídas a uma entidade e, portanto, o acesso de navegação é concedido no nível do modelo.  
  
 ![mds_conc_inheritance_model](../master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **Entidades**  
  
 Quando você atribui permissão a uma entidade, seus membros folha ou seus membros consolidados, o acesso de navegação significa que você pode ler ou atualizar o nome e o código de todos os membros. Você também pode ler o nome do modelo.  
  
 **Atributos**  
  
 Quando você atribui permissão a um atributo, o acesso de navegação significa que você pode ler ou atualizar o nome e o código de todos os membros da entidade. Você também pode ler o nome do modelo.  
  
 **Coleções**  
  
 Quando atribui permissões a coleções, você pode ler ou atualizar o nome, o código, a descrição e a ID do proprietário. Você também pode ler o nome do modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  

