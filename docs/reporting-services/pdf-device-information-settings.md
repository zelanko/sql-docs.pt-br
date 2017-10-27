---
title: "Configurações de informações do dispositivo PDF | Microsoft Docs"
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
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e02ae92cfb973c7287fde080628fcc26cb784276
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="pdf-device-information-settings"></a>Configurações de informações do dispositivo PDF
  A tabela a seguir lista as configurações de informações de dispositivo para a renderização de relatórios no formato PDF.  
  
|Configuração|Value|  
|-------------|-----------|  
|**Colunas**|O número de colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**ColumnSpacing**|O espaçamento entre colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**DpiX**|A resolução do dispositivo de saída em direção de x.|  
|**DpiY**|A resolução do dispositivo de saída em direção de y.|  
|**EndPage**|A última página do relatório a ser renderizado. O valor padrão é o valor de **StartPage**.|  
|**HumanReadablePDF**|Indica se o PDF deve ser compactado, permitindo que a origem fique mais legível. O valor padrão é **false.**|  
|**MarginBottom**|O valor da margem inferior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginLeft**|O valor da margem esquerda, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginRight**|O valor da margem direita, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginTop**|O valor da margem superior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**PageHeight**|A altura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 11in). Esse valor substitui as configurações originais do relatório.|  
|**PageWidth**|A largura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido por um "in" (por exemplo, 8,5in). Esse valor substitui as configurações originais do relatório.|  
|**StartPage**|A primeira página do relatório a ser renderizada. O valor **0** indica que todas as páginas serão renderizadas. O valor padrão é **1**.|  
  
## <a name="see-also"></a>Consulte também  
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em rsreportserver. config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40; SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  

