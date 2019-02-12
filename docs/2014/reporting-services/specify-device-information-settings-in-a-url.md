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
manager: kfile
ms.openlocfilehash: d769e272792bb4032c2ad2f0d5469e33a512656b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012567"
---
# <a name="specify-device-information-settings-in-a-url"></a>Especificar configurações de informações do dispositivo em uma URL
  As configurações de informações de dispositivo são parâmetros que são passados para uma extensão de renderização. Se você usar os métodos do serviço Web do servidor de relatório do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para renderizar um relatório, um elemento XML `DeviceInfo` será passado como um parâmetro de entrada. Os elementos filhos do elemento `DeviceInfo` são específicos para as configurações de informações de dispositivo de extensões de renderização diferentes. Você pode incluir as configurações de informações de dispositivo em uma URL usando a cadeia de caracteres do parâmetro *rc:tag=value* , em que *tag* é o nome do elemento de configurações de informações de dispositivo que estão sendo acessados. Para obter mais informações sobre configurações de informações de dispositivo o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte [Passando configurações de informações de dispositivos para extensões de renderização](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
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
  
  
