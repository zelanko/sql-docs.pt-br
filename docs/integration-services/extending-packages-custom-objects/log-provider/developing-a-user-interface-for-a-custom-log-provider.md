---
title: Desenvolver uma interface do usuário para um provedor de logs personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom log providers
- custom log providers [Integration Services], developing custom user interface
ms.assetid: 6fd2d269-d87a-4134-82a1-40a09b3b5453
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fccc03acb846fe1fe7db12d339c633b7d4c7e306
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297136"
---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>Desenvolvendo uma interface do usuário para um provedor de logs personalizado

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Muitos provedores de log do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] têm uma interface do usuário personalizada que implementa o <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> e substitui a caixa de texto **Configuração** na caixa de diálogo **Configurar Logs de SSIS** por uma lista suspensa filtrada com gerenciadores de conexões disponíveis. Porém, interfaces do usuário personalizadas para provedores de log personalizados não são implementadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um provedor de logs personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [Codificar um provedor de log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
  
  
