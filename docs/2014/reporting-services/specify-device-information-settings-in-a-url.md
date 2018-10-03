---
title: Especificar configurações de informações de dispositivo em uma URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 061fc6edeec6e3970ade638115b3d28389218a3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067816"
---
# <a name="specify-device-information-settings-in-a-url"></a>Especificar configurações de informações do dispositivo em uma URL
  As configurações de informações de dispositivo são parâmetros que são passados para uma extensão de renderização. Se você usar os métodos do serviço Web do servidor de relatório do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para renderizar um relatório, um elemento XML `DeviceInfo` será passado como um parâmetro de entrada. Elementos filho do `DeviceInfo` elemento são específicas para as configurações de informações do dispositivo de extensões de renderização diferentes. Você pode incluir as configurações de informações de dispositivo em uma URL usando a cadeia de caracteres do parâmetro *rc:tag=value* , em que *tag* é o nome do elemento de configurações de informações de dispositivo que estão sendo acessados. Para obter mais informações sobre as configurações de informações do dispositivo no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte [passando configurações de informações de dispositivo para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir define o formato do relatório especificado para JPEG usando a configuração de informações do dispositivo *OutputFormat* da extensão de renderização de imagem (as quebras de linha foram adicionadas para legibilidade):  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>Consulte também  
 [Acesso à URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](url-access-parameter-reference.md)  
  
  
