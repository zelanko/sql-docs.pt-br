---
title: "Visão geral das extensões de renderização | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- formats [Reporting Services], rendering extensions
- rendering extensions [Reporting Services], about extensions
ms.assetid: 909356a0-4709-43e5-b597-33bd9bb22882
caps.latest.revision: "41"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 3ab1065adff87ee843e649b7da2b8d6a21d4b1ac
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="rendering-extensions-overview"></a>Visão geral das extensões de renderização
  Uma extensão de renderização é um componente ou um módulo de um servidor de relatório que transforma dados de relatório e informações de layout para um formato específico do dispositivo. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui sete extensões de renderização: HTML, Excel, Word, CSV ou Texto, XML, Imagem e PDF. Você pode criar extensões de renderização adicionais para gerar relatórios em outros formatos.  
  
> [!NOTE]  
>  Para determinar quais extensões de renderização estão disponíveis, exiba a lista das extensões instaladas no arquivo RSReportServer.config.  
  
 A tabela a seguir descreve as extensões de renderização incluídas no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Nome da Extensão|Description|  
|--------------------|-----------------|  
|**XML**|Renderiza um relatório em XML. O relatório é aberto em um navegador. Transformações adicionais aplicadas a esta saída XML podem ser uma forma econômica de evitar o desenvolvimento de sua própria extensão de renderização.|  
|**CSV**|Renderiza um relatório em um formato delimitado por vírgula. O relatório é aberto em uma ferramenta de visualização associada a formatos de arquivo CSV.|  
|**IMAGE**|Renderiza um relatório em um formato orientado para páginas. O formato é mostrado como **TIFF** na lista suspensa Exportar da barra de ferramentas de relatório.|  
|**PDF**|Renderiza um relatório no Adobe Acrobat Reader. O formato é mostrado como **Arquivo Acrobat (PDF)** na lista suspensa Exportar da barra de ferramentas de relatório.|  
|**EXCEL**|Renderiza um relatório no [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)].|  
|**WORD**|Renderizar um relatório no [!INCLUDE[ofprword](../../../includes/ofprword-md.md)].|  
|**HTML 4.0** (parte da extensão de renderização HTML)|HTML é o formato usado para renderizar inicialmente o relatório. Se o seu navegador der suporte a HTML 4.0, esse será o formato usado. Caso contrário, o HTML 3.2 será usado.|  
|**MHTML** (parte da extensão de renderização HTML)|Renderiza um relatório em MHTML. O relatório é aberto no Internet Explorer. O formato é mostrado como **Arquivo Web** na lista suspensa Exportar da barra de ferramentas de relatório.|  
|**NULL**|Não renderiza um relatório para um formato específico. Essa extensão de renderização é útil para colocar relatórios em cache. A renderização nula deve ser usada em conjunto com uma execução ou entrega agendada.|  
  
 Para obter mais informações sobre os formatos recomendados e seus usos, consulte [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
 Cada uma das extensões de renderização implementadas pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e enviadas com o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa um conjunto comum de interfaces. Isso garante que cada extensão implemente funcionalidade comparável e reduz a complexidade do código de renderização no núcleo do servidor de relatório.  
  
## <a name="rendering-object-model"></a>Modelo de objeto de renderização  
 Quando um relatório é processado, o resultado é um modelo de objeto publicamente exposto conhecido como ROM (Modelo de Objeto de Renderização). O Modelo de Objeto de Renderização é uma coleção de classes que definem os conteúdos, o layout e os dados de um relatório que foi processado. O ROM está disponível para desenvolvedores que queiram criar, desenvolver e implantar extensões de renderização personalizadas para o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. O ROM é gerado quando o servidor de relatório processa a definição XML de um relatório junto com os dados de relatório definidos pelo usuário. Quando o processamento é concluído, o modelo de objeto público é usado por uma extensão de renderização para definir a saída do relatório. As classes públicas disponíveis do ROM são definidas no namespace **Microsoft.ReportingServices.OnDemandReportRendering**.  
  
## <a name="writing-custom-rendering-extensions"></a>Escrevendo extensões de renderização personalizadas  
 Antes de decidir criar uma extensão de renderização personalizada, avalie alternativas mais simples. Você pode:  
  
-   Personalizar a saída renderizada especificando configurações de informações de dispositivo para extensões existentes.  
  
-   Adicione formatação personalizada e recursos de apresentação combinando XSLT (Transformações XSL) com a saída do formato de renderização XML.  
  
 Escrever uma extensão de renderização personalizada é difícil. Normalmente, uma extensão de renderização deve dar suporte a todas as combinações possíveis de elementos de relatório e exige que você implemente centenas de classes, de interfaces, de métodos e de propriedades. Se precisar renderizar um relatório em um formato não incluído no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e decidir escrever sua própria implementação de código gerenciado de uma extensão de renderização, o código da extensão de renderização deverá implementar a interface **Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension**, que é exigida pelo servidor de relatório.  
  
 Para obter a documentação e whitepapers suplementares sobre o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], consulte os últimos recursos técnicos no [site do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=19951).  
  
## <a name="see-also"></a>Consulte também  
 [Implementando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
