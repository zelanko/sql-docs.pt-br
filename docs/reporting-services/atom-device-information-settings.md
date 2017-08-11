---
title: "Configurações de informações do dispositivo ATOM | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 847b387a04f302c731ed3cb1d2c31df57e202680
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="atom-device-information-settings"></a>Configurações de informações do dispositivo ATOM
  As configurações das informações de dispositivo para a extensão de renderização Atom dão suporte ao envio do nome de um feed Atom e de uma codificação de caracteres a ser usada.  
  
 A tabela a seguir lista as configurações de informações de dispositivo para renderização para um documento de serviço de dados.  
  
|Configuração|Value|  
|-------------|-----------|  
|**DataFeed**|Se for especificado, renderiza o feed Atom que corresponde ao nome do feed fornecido nessa configuração. Se não, renderiza o documento do serviço Atom para o relatório. O identificador exclusivo gerado automaticamente do feed de dados. Este valor é usado internamente e você não deve alterar isto.|  
|**Codificação**|O nome da IANA (Internet Assigned Numbers Authority) de uma codificação de caracteres com suporte do .NET Framework. O valor padrão é **UTF-8**. Exemplos de outros valores incluem ASCII, UTF-7 e UTF-16.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em rsreportserver. config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40; SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
