---
title: Configurações de informações de dispositivo PDF | Microsoft Docs
ms.date: 03/16/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], PDF rendering
- PDF [Reporting Services]
ms.assetid: 9a4aabe5-dbdc-4884-b999-1200983fee47
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5442980dd2f67cf72e301a82ae3730f90a173116
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "70911324"
---
# <a name="pdf-device-information-settings"></a>Configurações de informações do dispositivo PDF
  A tabela a seguir lista as configurações de informações de dispositivo para a renderização de relatórios no formato PDF.  
  
|Configuração|Valor|  
|-------------|-----------|  
| **AccessiblePDF** | Indica se é necessário renderizar um PDF acessível/marcado, que é maior em tamanho, mas permite uma leitura e navegação mais fácil em leitores de tela e outras tecnologias adaptativas. O valor padrão é **false**. [Disponível no Servidor de Relatórios do Power BI (março de 2018) e mais recente] |
|**Colunas**|O número de colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**ColumnSpacing**|O espaçamento entre colunas a ser definido para o relatório. Esse valor substitui as configurações originais do relatório.|  
|**DpiX**|A resolução do dispositivo de saída em direção de x.|  
|**DpiY**|A resolução do dispositivo de saída em direção de y.|  
|**EmbedFonts**|Indica se as fontes devem ser inseridas no arquivo PDF. Inseri-las aumentará o tamanho do arquivo, mas as fontes de relatório serão renderizadas corretamente para todos os clientes. Um valor de **None** desabilita a incorporação de fonte.|  
|**EndPage**|A última página do relatório a ser renderizado. O valor padrão é o valor de **StartPage**.|  
|**HumanReadablePDF**|Indica se um arquivo PDF descompactado deve ser renderizado; esse PDF é maior em tamanho, porém mais legível por humanos em um editor de texto sem formatação. O valor padrão é **false.**|  
|**MarginBottom**|O valor da margem inferior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginLeft**|O valor da margem esquerda, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginRight**|O valor da margem direita, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**MarginTop**|O valor da margem superior, em polegadas, a ser definido para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 1in). Esse valor substitui as configurações originais do relatório.|  
|**PageHeight**|A altura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido de "in" (por exemplo, 11in). Esse valor substitui as configurações originais do relatório.|  
|**PageWidth**|A largura da página, em polegadas, a ser definida para o relatório. Inclua um valor inteiro ou um decimal seguido por um "in" (por exemplo, 8,5in). Esse valor substitui as configurações originais do relatório.|  
|**StartPage**|A primeira página do relatório a ser renderizada. O valor **0** indica que todas as páginas serão renderizadas. O valor padrão é **1**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar parâmetros de extensão de renderização em RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referência técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
