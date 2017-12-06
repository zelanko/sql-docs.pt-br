---
title: "Removendo uma extensão de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: "31"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2d03cb6841433eca5bce20348eb6ffac18b90e11
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="removing-a-delivery-extension"></a>Removendo uma extensão de entrega
  Para remover uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta remover o elemento **Extension** da extensão de entrega do arquivo de configuração. Depois que as informações de configuração forem removidas, a extensão de entrega não estará mais disponível para o servidor de relatório.  
  
 Depois que o elemento **Extension** correspondente de uma extensão de entrega é removido do arquivo de configuração, ele não fica mais registrado no servidor de relatório. O servidor de relatório remove a entrada da lista de extensões de entrega e desativa quaisquer assinaturas que usem aquela extensão de entrega. Quando uma extensão de entrega é removida, os usuários não podem mais selecioná-la como um método de notificação.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
