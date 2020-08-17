---
description: Permissões de área funcional (Master Data Services)
title: Permissões de área funcional
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- functional area permissions [Master Data Services], about functional area permissions
- functional area permissions [Master Data Services]
- permissions [Master Data Services], functional areas
ms.assetid: a80b87b3-b904-4cda-8582-0761c2617c57
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0f3f863a6c08de5a4194c9fd6a08e4ee3e207e50
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88388322"
---
# <a name="functional-area-permissions-master-data-services"></a>Permissões de área funcional (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  É possível atribuir permissão a cada uma das áreas funcionais da interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Estas são as áreas funcionais:  
  
-   **Explorer**  
  
-   **Gerenciamento de Versões**  
  
-   **Gerenciamento de Integração**  
  
-   **Administração do Sistema**  
  
-   **Permissões de Usuário e Grupo**  
  
-   **Superusuário**  
  
 Ao atribuir permissão a uma área funcional, você torna uma área da interface do usuário visível para o usuário ou grupo.  
  
 Na área funcional **Explorer** , permissões adicionais atribuídas a objetos de modelo e membros de hierarquia determinam quais dados que um usuário pode acessar. Dentro de todas as outras áreas funcionais, um usuário deve ser um administrador de modelo para exibir um modelo e agir sobre ele. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
> [!IMPORTANT]  
>  Um usuário com permissão de Superusuário efetivamente tem permissão de Administrador em todos os modelos e tem todas as outras permissões funcionais.  
  
 Um usuário ou grupo deve ter permissão a, pelo menos, uma área funcional e um modelo na guia **Modelos** para acessar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
