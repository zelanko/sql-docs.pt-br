---
title: "Aprovação necessária (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f73510c38944126f65567dcb0e6a8b97ec2498e0
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="approval-required-master-data-services"></a>Aprovação Necessária (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], o administrador pode definir uma entidade para a Aprovação Necessária. Todas as alterações nessa entidade exigiriam um dos administradores de entidade para revisar e aprovar as alterações.  
  
> [!NOTE]  
>  As alterações feitas nos membros folha requerem aprovação. As alterações feitas nas hierarquias explícitas preteridas e nas coleções ignoram a aprovação.  
>   
>  As alterações feitas pelo processo da tabela de preparo ignoram a aprovação.  
>   
>  As alterações feitas por uma regra de negócio ignoram a aprovação.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional da Administração do Sistema.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Uma entidade deve existir. Para obter mais informações, consulte [Criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="to-enable-approval-required-for-an-entity"></a>Para habilitar a Aprovação Necessária para uma entidade  
  
1.  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , da grade, selecione a linha da entidade para a qual você deseja habilitar a  **Aprovação Necessária** .  
  
4.  Clique em **Editar**, escolha **Aprovação Necessária**e, em seguida, clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de alterações &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md)  
  
  
