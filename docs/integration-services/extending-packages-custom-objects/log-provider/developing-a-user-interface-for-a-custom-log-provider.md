---
title: Desenvolver uma interface do usuário para um provedor de logs personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-custom-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services], custom log providers
- custom log providers [Integration Services], developing custom user interface
ms.assetid: 6fd2d269-d87a-4134-82a1-40a09b3b5453
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c9705b17884585ab43b8f4848a19ee44140e39ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>Desenvolvendo uma interface do usuário para um provedor de logs personalizado
  Muitos provedores de log do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] têm uma interface do usuário personalizada que implementa o <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> e substitui a caixa de texto **Configuração** na caixa de diálogo **Configurar Logs de SSIS** por uma lista suspensa filtrada com gerenciadores de conexões disponíveis. Porém, interfaces do usuário personalizadas para provedores de log personalizados não são implementadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um provedor de logs personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [Codificar um provedor de log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
  
  
