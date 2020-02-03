---
title: Removendo uma extensão de entrega | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 49b36598d643bd88496117655f23f642e663d04c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63193728"
---
# <a name="removing-a-delivery-extension"></a>Removendo uma extensão de entrega
  Para remover uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta remover o elemento **Extension** da extensão de entrega do arquivo de configuração. Depois que as informações de configuração forem removidas, a extensão de entrega não estará mais disponível para o servidor de relatório.  
  
 Depois que o elemento **Extension** correspondente de uma extensão de entrega é removido do arquivo de configuração, ele não fica mais registrado no servidor de relatório. O servidor de relatório remove a entrada da lista de extensões de entrega e desativa quaisquer assinaturas que usem aquela extensão de entrega. Quando uma extensão de entrega é removida, os usuários não podem mais selecioná-la como um método de notificação.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementando uma extensão de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
