---
title: "Desenvolvendo uma Interface de usuário para um provedor de Log personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 014e4387d80236898d7d6b7a10c992de933da2c4
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>Desenvolvendo uma interface do usuário para um provedor de logs personalizado
  Muitos [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] provedores de log tem uma interface de usuário personalizada que implementa <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> e substitui o **configuração** caixa de texto de **configurar Logs de SSIS** caixa de diálogo com uma lista suspensa filtrada de gerenciadores de conexão disponíveis. No entanto, interfaces do usuário personalizadas para provedores de log personalizados não são implementadas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Criando um provedor de Log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [Codificando um provedor de Log personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
  
  
