---
title: Removendo uma extensão de entrega | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7c4320f46b5013b0fa2accbc81792748c2d9f384
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63164019"
---
# <a name="removing-a-delivery-extension"></a>Removendo uma extensão de entrega
  Para remover uma extensão de entrega do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta remover o elemento **Extension** da extensão de entrega do arquivo de configuração. Depois que as informações de configuração forem removidas, a extensão de entrega não estará mais disponível para o servidor de relatório.  
  
 Depois que o elemento **Extension** correspondente de uma extensão de entrega é removido do arquivo de configuração, ele não fica mais registrado no servidor de relatório. O servidor de relatório remove a entrada da lista de extensões de entrega e desativa quaisquer assinaturas que usem aquela extensão de entrega. Quando uma extensão de entrega é removida, os usuários não podem mais selecioná-la como um método de notificação.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementando uma extensão de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensões do Reporting Services](../reporting-services-extension-library.md)  
  
  
